<!---
  功能：功能描述
  作者：woods.qiu
  时间：2021年03月24日 20:06:07
  版本：v1.0
  修改记录：
  修改内容：
  修改人员：
  修改时间： 线条弯曲
-->
<template>
  <div class="container">
    <el-card class="box-card" style="position: absolute;width: 450px;top: 0;right: 0;">
      <div slot="header" class="clearfix">
        <span>节点信息</span>
        <!-- <el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button> -->
      </div>
      <div v-if="form.partyName" class="text item">
        <div class="opt">
          <el-form ref="form" :model="form" label-width="80px">
            <el-form-item label="零售户">
              <el-input v-model="form.partyName" disabled />
            </el-form-item>
            <el-form-item label="当事人">
              <el-input v-model="form.partyIsCust" disabled />
            </el-form-item>
            <el-form-item label="查询条件">
              <el-select v-model="form.opts" placeholder="请选择活动区域">
                <el-option label="手机号" value="shanghai" />
                <el-option label="专卖证" value="beijing" />
                <el-option label="同案" value="beijing" />
                <el-option label="涉案" value="beijing" />
              </el-select>
            </el-form-item>
            <el-form-item label="时间">
              <el-col :span="11">
                <el-date-picker v-model="form.start" type="date" placeholder="选择开始日期" style="width: 100%;" />
              </el-col>
              <el-col style="text-align: center;" class="line" :span="2">-</el-col>
              <el-col :span="11">
                <el-date-picker v-model="form.end" placeholder="选择结束时间" style="width: 100%;" />
              </el-col>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" size="mini">搜索</el-button>
            </el-form-item>
          </el-form>
        </div>
      </div>
      <div v-else>
        <p style="color: #999;">请点击零售户人名查询</p>
      </div>
    </el-card>
  </div>
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
      simulation: null,
      form: {
        partyName: '',
        partyIsCust: '',
        opts: '',
        start: new Date(),
        end: new Date()
      }
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
        .force('link', d3.forceLink(links).id(d => d.rowId).distance(180).strength(0.1)) // 弹簧力
        .force('charge', d3.forceManyBody()) // 电荷力[吸引力]
        .force("x", d3.forceX())
        .force("y", d3.forceY())
        .force('collision', d3.forceCollide(r * 2)) // 碰撞检测
        .force('center', d3.forceCenter(width / 2, height / 2)) // 向心力

      const svg = d3.select('.container')
        .append('svg')
        .style("font", '12px sans-serif')
        .style('width', 750)
        .style('height', 500)
        .style('position', 'absolute')
        .style('top', '50%')
        .style('left', '40%')
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
      const markerPre = svg.append('defs')
        .append('marker')
        .attr('id', 'arrowPre')
        .attr('stroke-width', 1)
        .attr('markerUnits', 'strokeWidth')
        .attr('markerUnits', 'userSpaceOnUse')
        .attr('viewBox', '0 -5 10 10')
        .attr('refX', 40)
        .attr('refY', -3)
        .attr('markerWidth', 10)
        .attr('markerHeight', 12)
        .attr('orient', 'auto')
        .append('path')
        .attr('d', 'M 0 -3 L 11 -1 L 1 5')
        .attr('fill', '#999')
        .attr('stroke-opacity', 0.6)

      const markerNext = svg.append('defs')
        .append('marker')
        .attr('id', 'arrowNext')
        .attr('stroke-width', 1)
        .attr('markerUnits', 'strokeWidth')
        .attr('markerUnits', 'userSpaceOnUse')
        .attr('viewBox', '0 -5 10 10')
        .attr('refX', 40)
        .attr('refY', -2.5)
        .attr('markerWidth', 10)
        .attr('markerHeight', 12)
        .attr('orient', 'auto')
        .append('path')
        .attr('d', 'M 2 -3 L 11 0 L 3 5')
        .attr('fill', '#999')
        .attr('stroke-opacity', 0.6)

      const g = svg.append('g')

      this.links = g.append('g')
        .attr('fill', 'none')
        .attr('stroke-width', 0.5)
        .attr('stroke', '#999')
        .attr('stroke-opacity', 0.6)
        .attr('marker-end', 'url(#arrowPre)')
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
        .style('fill', '#000')
        .style('font-size', 12)
        .style('font-weight', 500)
        .append('textPath')
        .attr('xlink:href', d => '#' + d.parentId + '_' + d.caseRelation + '_' + d.type)
        .attr('startOffset', '50%')
        .text(d => d.caseRelation + '·' + d.type)

      this.nodes = g.append('g')
        .attr('stroke', '#FFF')
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
          .attr('d', (d) => {
            const r = Math.hypot(d.target.x - d.source.x, d.target.y - d.source.y)

            if (d.source.x < d.target.x) {
            // return 'M' + d.source.x + ' ' + d.source.y + ' L' +  d.target.x + ' ' + d.target.y
              return `
              M${d.source.x},${d.source.y}
              A${r},${r} 0 0,1 ${d.target.x},${d.target.y}
            `
            } else {
            // return 'M' + d.target.x + ' ' + d.target.y + ' L' +  d.source.x + ' ' + d.source.y
              return `
              M${d.target.x},${d.target.y}
              A${r},${r} 1 0,1 ${d.source.x},${d.source.y}
            `
            }
          })
          .attr('marker-end', (d) => {
            if (d.source.x < d.target.x) {
              return 'url(#arrowNext)'
            } else {
              return null
            }
          })
          .attr('marker-start', (d) => {
            if (d.source.x < d.target.x) {
              return null
            } else {
              return 'url(#arrowPro)'
            }
          })

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
        .attr('fill', 'none')
        .attr('stroke', '#999')
        .attr('stroke-width', 1)
        .attr('marker-end', 'url(#arrowPre)')
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
        .style('fill', '#000')
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
      this.form.partyName = items.partyName
      this.form.partyIsCust = items.partyIsCust
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
ul li {
  list-style: none;
}
.left {
  display: inline-block;
  width: 70px;
  text-align: right;
}
.right {
  display: inline-block;
}
</style>
