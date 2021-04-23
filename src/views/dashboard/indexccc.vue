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
    <svg>
      <!-- <path d="M50 50 V 150 H 300 V 50 Z" />
      <circle cx="50" cy="50" r="2" fill="red"/>
      <circle cx="50" cy="150" r="2" fill="red"/>
      <circle cx="300" cy="50" r="2" fill="red"/>
      <circle cx="300" cy="150" r="2" fill="red"/> -->

      <path d="M130 110 C 140 170, 250 150, 250 110" stroke="black" fill="transparent" />

      <path d="M50 50 L 80 0 L 80 30" />

      <!--
        Q: 二次贝塞尔曲线 x1 y1, x y
       -->
      <path d="M10 80 Q 95 20 180 80" stroke="red" fill="transparent" />

      <!--
        A：rx ry x-axis-rotation large-arc-flag sweep-flag x y
        large-arc-flag（角度大小）
        sweep-flag（弧线方向）
        arge-arc-flag决定弧线是大于还是小于180度
        -->
      <path d="M10 315 A 30 50 0 0 1 162.55 162.45" stroke="orangered" fill="transparent" />

      <g>
        <path d="M10,30 A20,20,0,0,1,50,30 A20,20,0,0,1,90,30 Q90,60,50,90 Q10,60,10,30 Z" />
        <circle cx="20" cy="20" r="2" fill="red" />
        <circle cx="50" cy="30" r="2" fill="red" />
        <circle cx="90" cy="30" r="2" fill="red" />
        <circle cx="90" cy="60" r="2" fill="red" />
        <circle cx="50" cy="90" r="2" fill="red" />
        <circle cx="10" cy="60" r="2" fill="red" />
        <circle cx="10" cy="30" r="2" fill="red" />
      </g>

      <clipPath id="myClip" clipPathUnits="objectBoundingBox">
        <circle cx=".5" cy=".5" r=".5" />
      </clipPath>

      <!-- <circle cx="60" cy="60" r="40" fill="RGB(222,212,238)" />
      <circle cx="60" cy="60" r="32" stroke="#F5003C" stroke-width="8" fill="RGB(222,212,238)"/> -->

      <circle cx="40" cy="40" r="40" fill="RGB(222,212,238)" />
      <path d="M 40 8 A 32 32, 0, 0, 1, 45, 8.9" stroke="#F5003C" stroke-width="8" fill="RGB(222,212,238)" />
      <circle cx="40" cy="40" r="2" />
    </svg>
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
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {

  },
  beforeDestroy() {},
  methods: {
  }
}
</script>

<style>

/* 如果浏览器支持几何属性 r，可以加一点 css */

@keyframes openYourHeart {from {r: 0} to {r: 60px}}

#myClip circle {
  animation: openYourHeart 15s infinite;
}
</style>
