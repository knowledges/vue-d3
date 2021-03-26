<template>
  <div class="dashboard-container" />
</template>

<script>
import * as d3 from 'd3'
export default {
  name: 'Dashboard',
  data() {
    return {
      r: 20,
      hierarchy: {
        'name': 'Eve',
        'children': [
          {
            'name': 'Seth'
          },
          {
            'name': 'Abel'
          },
          {
            'name': 'Azura'
          }
        ]
      }
    }
  },
  mounted() {
    console.log('D3=>', d3)

    this.forceSimulation()
  },
  methods: {
    forceSimulation() {
      // create hierarchy
      const root = d3.hierarchy(this.hierarchy)
      const links = root.links()
      const nodes = root.descendants() //
      // create forceSimulation
      const simulation = d3.forceSimulation(nodes)
        .force('link', d3.forceLink(links).id(d => d.id).distance(this.r * 5).strength(1))
        .force('charge', d3.forceManyBody().strength(-50))
        .force('x', d3.forceX())
        .force('y', d3.forceY())
      console.log(d3.forceX(), d3.forceY())

      const svg = d3.select('div.dashboard-container')
        .append('svg')
        .attr('viewBox', [-600 / 2, -600 / 2, 600, 600])
      console.log('svg', svg)

      const link = svg.append('g')
        .attr('stroke', '#999')
        .attr('stroke-opacity', 0.6)
        .selectAll('line')
        .data(links)
        .join('line')

      console.log('link', link)

      const drag = (simulation) => {
        function dragstarted(event, d) {
          if (!event.active) simulation.alphaTarget(0.3).restart()
          d.fx = d.x
          d.fy = d.y
        }

        function dragged(event, d) {
          d.fx = event.x
          d.fy = event.y
        }

        function dragended(event, d) {
          if (!event.active) simulation.alphaTarget(0)
          d.fx = null
          d.fy = null
        }

        return d3.drag()
          .on('start', dragstarted)
          .on('drag', dragged)
          .on('end', dragended)
      }

      const node = svg.append('g')
        .attr('fill', '#fff')
        .attr('stroke', '#000')
        .attr('stroke-width', 0.5)
        .selectAll('circle')
        .data(nodes)
        .join('circle')
        .attr('fill', d => d.children ? null : '#000')
        .attr('stroke', d => d.children ? null : '#fff')
        .attr('cx', (d, i) => {
          return d.cx
        })
        .attr('cy', (d, i) => {
          return d.cy
        })
        .attr('r', this.r)
        .call(drag(simulation))

      console.log('node', node)

      // TODO 遗留问题， line[x1\x2,y1\y2] circle [cx\cy] 缺失参数

      node.append('title')
        .text(d => d.data.name)

      simulation.on('tick', () => {
        link.attr('x1', d => d.source.x)
          .attr('y1', d => d.source.y)
          .attr('x2', d => d.target.x)
          .attr('y2', d => d.target.y)

        node.attr('cx', d => d.x)
          .attr('cy', d => d.y)
      })

      // invalidation.then(() => simulation.stop());

      return svg.node()
    },
    createSVG() {
      d3.select('div.dashboard-container')
        .append('svg')
        .attr('class', 'svg')
        .attr('width', 960)
        .attr('height', 500)
        .attr('x', 20)
        .attr('y', 20)
        .style('background', '#FFF')
    },
    marker() {
      d3.select('svg.svg')
        .append('defs')
        .append('marker')
        .attr('markerWidth', 10)
        .attr('markerHeight', 10)
        .attr('refX', 0)
        .attr('refY', 4)
        .attr('orient', 'auto')
        .append('path')
        .attr('d', 'M 0 0 100 100 0 80')
        .style('fill:none;stroke:black;')
    },
    polygon() {
      // pass
    },
    createCircleGroup() {
      const outerG = d3.selectAll('svg.svg')
        // .append('defs')
        .append('g')
        .attr('id', 'myCircleGroup')

      outerG.append('circle')
        .attr('cx', 50)
        .attr('cy', 50)
        .attr('r', 30)

      outerG.append('text')
        .attr('x', 30)
        .attr('y', 30)
        .attr('pointer-events', 'none')
        .attr('text-anchor', 'middle')
        .text('woods.qiu')
    },
    circle() {
      d3.select('svg.svg')
        .append('circle')
        .attr('cx', 100)
        .attr('cy', 100)
        .attr('r', 40)
        .attr('fill', 'violet')
        .attr('fill-opacity', 0.7)
        .attr('stroke', 'white')
        .attr('stroke-width', 2)
        .on('click', function(e) {
          console.log(e)
        })
    },
    line() {
      d3.select('svg.svg')
        .append('line')
        // .attr('stroke-dasharray', 10) // 偶数为虚线
        .attr('stroke-width', 5)
        .attr('stroke', 'green')
        .attr('stroke-linejoin', 'bevel')
        .attr('x1', 0)
        .attr('y1', 0)
        .attr('x2', 300)
        .attr('y2', 300)
    },
    rect() {
      d3.select('svg.svg')
        .append('g')
        .attr('transform', 'translate(20,20)')
        .append('rect')
        .attr('width', 920)
        .attr('height', 460)
    },
    seelctAllP() {
      d3.selectAll('p')
        .attr('class', 'graf')
        .style('color', 'red')
    },
    enterPAppent() {
      // 如果 P 标签 大于 data 数组个数。在末尾插入P标签
      d3.select('div')
        .selectAll('p')
        .data([4, 8, 15, 16, 23, 42])
        .style('font-size', function(d) { return d + 'px' })
        .enter().append('p')
        .text(function(d) { return 'I’m number ' + d + '!' })
    }
  }
}
</script>

<style>
/* circle {
  stroke-width: 3;
  stroke: #f00;
  fill-opacity: 0.5;
  fill: #f00;
}

circle:hover {
  stroke: #f00;
  fill-opacity: 0.4;
  fill: #f00;
}

g {
  cursor: pointer;
}

text {
  font-weight: 'nromal';
  stroke: #FFF;
  font-size: 12px;
  text-anchor: middle;
  dominant-baseline: middle;
}

.red {
  fill: red;
}

.fancy {
  fill: none;
  stroke: black;
  stroke-width: 3pt;
} */
</style>
