<!---
  功能：功能描述
  作者：woods.qiu
  时间：2021年03月24日 20:06:07
  版本：v1.0
  修改记录：
  修改内容：
  修改人员：
  修改时间：2021-3-30 09:58:50
-->
<template>
  <div class="container" />
</template>

<script>
import * as d3 from 'd3'
import axios from 'axios'
export default {
  name: 'Index',
  components: {},
  props: {},
  data() {
    return {
      dataList: {
        'nodes': [
          // { 'id': 'Myriel', 'group': 1 },
        ],
        'links': [
          // { 'source': 'Napoleon', 'target': 'Myriel', 'value': 2 }
        ]
      },
      colorList: ['rgb(241, 102, 103)', 'rgb(87, 199, 227)', 'rgb(243, 105, 36)', 'yellow', 'orange', 'brown', 'chartreuse', 'violet', 'tan', 'turquoise', 'springgreen'],
      condition: {
        r: 30,
        width: 600,
        height: 600
      },
      links: [],
      nodes: [],
      linksName: [],
      nodesName: [],
      simulation: null
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {
    axios.get('http://10.20.11.251:8084/szwm/neo/partytocase/selectPartyToCaseByCaseTimes?times=5')
      .then(response => {
        const data = response.data

        this.dataList.nodes = data.map((item) => {
          item.start.rowId = item.start.rowId.toString()
          return item.start
        })

        this.initGraph(this.dataList)
      })
  },
  beforeDestroy() {},
  methods: {
    initGraph(data) {
      const { width, height, r } = this.condition

      const links = data.links.map(d => Object.create(d))
      const nodes = data.nodes.map(d => Object.create(d))

      this.simulation = d3.forceSimulation(nodes)
        .force('link', d3.forceLink(links).id(d => d.rowId).distance(180))
        .force('charge', d3.forceManyBody())
        .force('collision', d3.forceCollide(r * 2))
        // .force('radial', d3.forceRadial(function(d) { return d.type === "a" ? 200 : 400; }))
        .force('center', d3.forceCenter(width / 2, height / 2))

      const svg = d3.select('.container')
        .append('svg')
        .style('width', 750)
        .style('height', 500)
        .style('position', 'absolute')
        .style('top', '50%')
        .style('left', '50%')
        .style('transform', 'translate(-50%, -50%)')
        .style('border-radius', '8px')
        .style('background-color', 'wheat')
        .style('background-repeat', 'no-repeat')
        .style('background-size', 'cover')
        .call(d3.zoom().on('zoom', function(e) {
          g.attr('transform', e.transform)
        }))

      /**
       * refx: 即箭头与线的偏移，0表示接触
       * refy: 一般设置为图形的一半，这样指示出来的比较顺眼
       * orient: 表示线的方向，一般设置为auto，表示跟随线的方向
       * markerWidth、markerHeight：marker大小
       * stroke-width: 线条粗细
       */
      const marker = svg.append('defs')
        .append('marker')
        .attr('id', 'arrow')
        .attr('stroke-width', 1)
        .attr('markerUnits', 'strokeWidth')
        .attr('markerUnits', 'userSpaceOnUse')
        .attr('viewBox', '0 -5 10 10')
        .attr('refX', 40)
        .attr('refY', 0)
        .attr('markerWidth', 10)
        .attr('markerHeight', 12)
        .attr('orient', 'auto')
        .append('path')
        .attr('d', 'M 0 -5 L 10 0 L 0 5')
        .attr('fill', '#999')
        .attr('stroke-opacity', 1)

      const g = svg.append('g')

      this.links = g.append('g')
        .attr('stroke-width', 0.5)
        .attr('stroke', '#999')
        .attr('stroke-opacity', 0.6)
        .attr('marker-end', 'url(#arrow)')
        .selectAll('path')
        .data(links)
        .join('path')
        .attr('stroke-width', 1)
        .attr('id', d => d.parentId + '_' + d.caseRelation + '_' + d.type)

      /**
       * 文字居中两个属性需要特别注意：
       * text-anchor：是指一个字符的坐标在这个字符中的位置
       * startOffset：是指字符在这个path中的位置，通过百分比表示
       */
      this.linksName = g.append('g')
        .selectAll('text')
        .data(links)
        .join('text')
        .style('text-anchor', 'middle')
        .style('fill', '#333')
        .style('font-size', 12)
        .style('font-weight', 500)
        .append('textPath')
        .attr('xlink:href', d => '#' + d.parentId + '_' + d.caseRelation + '_' + d.type)
        .attr('startOffset', '50%')
        .text(d => d.caseRelation + '·' + d.type)

      this.nodes = g.append('g')
        .attr('stroke', '#fff')
        .attr('stroke-width', 1.5)
        .selectAll('circle')
        .data(nodes)
        .join('circle')
        .attr('r', r)
        .attr('fill', this.color)
        .on('click', this.circleClk)
        .call(this.drag(this.simulation))

      this.nodes.append('title').text((d) => d.partyName || d.caseName)

      this.nodesName = g.append('g')
        .selectAll('text')
        .data(nodes)
        .join('text')
        .attr('class', 'node-text')
        .text((val) => {
          return this.textElipsis(val)
        })

      this.simulation.on('tick', () => {
        // 文字方向修改------文字方向永远处于可辨别方向
        this.links
          .attr('d', d => 'M' + d.source.x + ' ' + d.source.y + ' L' + d.target.x + ' ' + d.target.y)
        // this.links
        // .attr('d', (d) => {
        //   if (d.source.x < d.target.x) {
        //     return d=> 'M' + d.source.x + ' ' + d.source.y + ' L' +  d.target.x + ' ' + d.target.y
        //   } else {
        //     return d=> 'M' + d.target.x + ' ' + d.target.y + ' L' +  d.source.x + ' ' + d.source.y
        //   }
        // })

        this.nodes.attr('cx', d => d.x)
          .attr('cy', d => d.y)

        // 方法一
        this.nodesName.attr('x', d => d.x)
          .attr('y', d => d.y)
      })
    },

    updatedGraph(data) {
      const { r } = this.condition
      const links = data.links
      const nodes = data.nodes

      this.links = this.links
        .data(links)
        .enter()
        .append('path')
        .attr('stroke-width', 1)
        .attr('marker-end', 'url(#arrow)')
        .attr('id', (d) => d.parentId + '_' + d.caseRelation + '_' + d.type)
        .merge(this.links)

      /**
       * 文字居中两个属性需要特别注意：
       * text-anchor：是指一个字符的坐标在这个字符中的位置
       * startOffset：是指字符在这个path中的位置，通过百分比表示
       */
      this.linksName = this.linksName
        .data(links)
        .enter()
        .append('text')
        .style('text-anchor', 'middle')
        .style('fill', '#333')
        .style('font-size', 12)
        .style('font-weight', 500)
        .append('textPath')
        .attr('xlink:href', d => '#' + d.parentId + '_' + d.caseRelation + '_' + d.type)
        .attr('startOffset', '50%')
        .merge(this.linksName)
        .text(d => d.caseRelation + '·' + d.type)

      this.nodes = this.nodes
        .data(nodes)
        .enter()
        .append('circle')
        .attr('r', r)
        .attr('fill', this.color)
        .merge(this.nodes)
        .on('click', this.circleClk)
        .call(this.drag(this.simulation))

      this.nodes.append('title').text((d) => d.partyName || d.caseName) // TODO

      this.nodesName = this.nodesName
        .data(nodes)
        .enter()
        .append('text')
        .attr('class', 'node-text')
        .text((val) => {
          return this.textElipsis(val)
        })
        .merge(this.nodesName)

      //  重新初始化绑定力模型
      this.simulation.nodes(nodes)
      // 修改节点位置和速度的函数
      this.simulation.force('link', d3.forceLink(links).id(d => d.rowId).distance(180))
      // 电荷力模型: 电荷力是全局的: 每个节点都受到其他所有节点的影响，甚至他们处于不连通的子图
      this.simulation.force('charge', d3.forceManyBody())
      // 碰撞检测
      this.simulation.force('collision', d3.forceCollide(r * 2))
      this.simulation.alpha(1)
      this.simulation.restart()
    },

    /**
     * 颜色数组
     */
    color(d) {
      return this.colorList[d.group]
    },
    /**
     * 拖拽
     */
    drag(simulation) {
      function dragstarted(event) {
        if (!event.active) simulation.alphaTarget(0.3).restart()
        event.subject.fx = event.subject.x
        event.subject.fy = event.subject.y
      }

      function dragged(event) {
        event.subject.fx = event.x
        event.subject.fy = event.y
      }

      function dragended(event) {
        if (!event.active) simulation.alphaTarget(0)
        event.subject.fx = null
        event.subject.fy = null
      }

      return d3.drag()
        .on('start', dragstarted)
        .on('drag', dragged)
        .on('end', dragended)
    },
    /**
     * 点击事件 【注意：新版本返回的是2个对象】
     * @param target 当前元素
     * @param item 当前数据对象
     */
    circleClk(target, items) {
      console.log('点击人的信息', items)
      axios.get('http://10.20.11.251:8084/szwm/neo/partytocase/selectPartyToCaseByPartyId?rowId=' + items.rowId)
        .then(response => {
          const data = response.data
          // 重构 end 数组
          const array = data.map((item) => {
            item.end.rowId = item.end.rowId.toString()
            this.$set(item.end, 'caseRelation', item.caseRelation)
            this.$set(item.end, 'type', item.type)
            this.$set(item.end, 'parentId', item.rowId.toString())
            return item.end
          })
          // 重新指定关系
          for (let i = 0; i < array.length; i++) {
          //  线的关系 根据外层的rowId 建立
            const link = this.dataList.links.find(o => { return o.parentId === array[i].parentId })

            if (!link) {
              array[i].source = items.rowId.toString()
              array[i].target = array[i].rowId.toString()
              this.dataList.links.push(array[i])
            }

            //  全的关系 根据end 的 rowId 建立
            const node = this.dataList.nodes.find(o => { return o.rowId === array[i].rowId })

            if (!node) {
              this.dataList.nodes.push(array[i])
            }
          }
          this.updatedGraph(this.dataList)
        })
      // const data = [{ 'id': 'Mlle.Baptistine', 'group': 2 },
      //   { 'id': 'Mme.Magloire', 'group': 2 },
      //   { 'id': 'CountessdeLo', 'group': 2 },
      //   { 'id': 'Geborand', 'group': 2 }]
      // console.log(data)
      // // TODO 请求到的数据 重新渲染画布
      // setTimeout(() => {
      //   for (let i = 0; i < data.length; i++) {
      //     let flage = true

      //     for (let j = 0; j < this.dataList.nodes.length; j++) {
      //       if (data[i].id === this.dataList.nodes[j].id) {
      //         flage = false
      //         break
      //       }
      //     }

      //     if (flage) {
      //       this.dataList.nodes.push(data[i])
      //       this.dataList.links.push({
      //         source: item.id.toString(),
      //         target: data[i].id.toString(),
      //         value: 5,
      //         relationship: '涉案'
      //       })
      //     }
      //   }
      //   console.log('打印结果', this.dataList)
      //   this.updatedGraph(this.dataList)
      // }, 2000)
    },
    textElipsis(val) {
      var len = 0
      const innerText = val.partyName || val.caseName
      for (var i = 0; i < innerText.length; i++) {
        var a = innerText.charAt(i)
        if (a.match(/[^\x00-\xff]/ig) != null) {
          len += 2
        } else {
          len += 1
        }
      }
      if (len <= 8) {
        return innerText
      } else {
        const str = innerText.substring(0, 7)
        return str + '...'
      }
    }
  }
}
</script>

<style>
circle {
  stroke: #fff;
  stroke-width: 1.5;
}
circle:hover{
  stroke-width: 5
}
text {
  fill: #fff;
  font-size: 12px;
  text-anchor: middle;
  /* 文本水平居中 */
  dominant-baseline: middle;
  /* 文本垂直居中 */
}
</style>
<style scoped>
.condition {
  position: absolute;
  left: 0;
  top: 0;
  display: inline-block;
  width: 300px;
  height: 100%;
  background: #f1f2f3;
  padding: 5px;
}
.demonstration {
  line-height: 35px;
}
</style>
