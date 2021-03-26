<!---
  功能：功能描述
  作者：woods.qiu
  时间：2021年03月24日 20:06:07
  版本：v1.0
  修改记录：
  修改内容：
  修改人员：
  修改时间：
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
          // { 'id': 'Napoleon', 'group': 2 },
          // { 'id': 'Champtercier', 'group': 1 },
          // { 'id': 'Cravatte', 'group': 1 },
          // { 'id': 'Count', 'group': 1 },
          // { 'id': 'OldMan', 'group': 1 },
          // { 'id': 'Labarre', 'group': 2 },
          // { 'id': 'Valjean', 'group': 2 },
          // { 'id': 'Marguerite', 'group': 3 },
          // { 'id': 'Mme.deR', 'group': 2 },
          // { 'id': 'Isabeau', 'group': 2 },
          // { 'id': 'Gervais', 'group': 2 },
          // { 'id': 'Tholomyes', 'group': 3 },
          // { 'id': 'Listolier', 'group': 3 },
          // { 'id': 'Fameuil', 'group': 3 },
          // { 'id': 'Blacheville', 'group': 3 },
          // { 'id': 'Favourite', 'group': 3 },
          // { 'id': 'Dahlia', 'group': 3 },
          // { 'id': 'Zephine', 'group': 3 },
          // { 'id': 'Fantine', 'group': 3 },
          // { 'id': 'Mme.Thenardier', 'group': 4 },
          // { 'id': 'Thenardier', 'group': 4 },
          // { 'id': 'Cosette', 'group': 5 },
          // { 'id': 'Javert', 'group': 4 },
          // { 'id': 'Fauchelevent', 'group': 0 },
          // { 'id': 'Bamatabois', 'group': 2 },
          // { 'id': 'Perpetue', 'group': 3 },
          // { 'id': 'Simplice', 'group': 2 },
          // { 'id': 'Scaufflaire', 'group': 2 },
          // { 'id': 'Woman1', 'group': 2 },
          // { 'id': 'Judge', 'group': 2 },
          // { 'id': 'Champmathieu', 'group': 2 },
          // { 'id': 'Brevet', 'group': 2 },
          // { 'id': 'Chenildieu', 'group': 2 },
          // { 'id': 'Cochepaille', 'group': 2 },
          // { 'id': 'Pontmercy', 'group': 4 },
          // { 'id': 'Boulatruelle', 'group': 6 },
          // { 'id': 'Eponine', 'group': 4 },
          // { 'id': 'Anzelma', 'group': 4 },
          // { 'id': 'Woman2', 'group': 5 },
          // { 'id': 'MotherInnocent', 'group': 0 },
          // { 'id': 'Gribier', 'group': 0 },
          // { 'id': 'Jondrette', 'group': 7 },
          // { 'id': 'Mme.Burgon', 'group': 7 },
          // { 'id': 'Gavroche', 'group': 8 },
          // { 'id': 'Gillenormand', 'group': 5 },
          // { 'id': 'Magnon', 'group': 5 },
          // { 'id': 'Mlle.Gillenormand', 'group': 5 },
          // { 'id': 'Mme.Pontmercy', 'group': 5 },
          // { 'id': 'Mlle.Vaubois', 'group': 5 },
          // { 'id': 'Lt.Gillenormand', 'group': 5 },
          // { 'id': 'Marius', 'group': 8 },
          // { 'id': 'BaronessT', 'group': 5 },
          // { 'id': 'Mabeuf', 'group': 8 },
          // { 'id': 'Enjolras', 'group': 8 },
          // { 'id': 'Combeferre', 'group': 8 },
          // { 'id': 'Prouvaire', 'group': 8 },
          // { 'id': 'Feuilly', 'group': 8 },
          // { 'id': 'Courfeyrac', 'group': 8 },
          // { 'id': 'Bahorel', 'group': 8 },
          // { 'id': 'Bossuet', 'group': 8 },
          // { 'id': 'Joly', 'group': 8 },
          // { 'id': 'Grantaire', 'group': 8 },
          // { 'id': 'MotherPlutarch', 'group': 9 },
          // { 'id': 'Gueulemer', 'group': 4 },
          // { 'id': 'Babet', 'group': 4 },
          // { 'id': 'Claquesous', 'group': 4 },
          // { 'id': 'Montparnasse', 'group': 4 },
          // { 'id': 'Toussaint', 'group': 5 },
          // { 'id': 'Child1', 'group': 10 },
          // { 'id': 'Child2', 'group': 10 },
          // { 'id': 'Brujon', 'group': 4 },
          // { 'id': 'Mme.Hucheloup', 'group': 8 }
        ],
        'links': [
          // { 'source': 'Napoleon', 'target': 'Myriel', 'value': 2 }
          // { 'source': 'Mlle.Baptistine', 'target': 'Myriel', 'value': 8 },
          // { 'source': 'Mme.Magloire', 'target': 'Myriel', 'value': 10 },
          // { 'source': 'Mme.Magloire', 'target': 'Mlle.Baptistine', 'value': 6 },
          // { 'source': 'CountessdeLo', 'target': 'Myriel', 'value': 1 },
          // { 'source': 'Geborand', 'target': 'Myriel', 'value': 1 },
          // { 'source': 'Champtercier', 'target': 'Myriel', 'value': 1 },
          // { 'source': 'Cravatte', 'target': 'Myriel', 'value': 1 },
          // { 'source': 'Count', 'target': 'Myriel', 'value': 2 },
          // { 'source': 'OldMan', 'target': 'Myriel', 'value': 1 },
          // { 'source': 'Valjean', 'target': 'Labarre', 'value': 1 },
          // { 'source': 'Valjean', 'target': 'Mme.Magloire', 'value': 3 },
          // { 'source': 'Valjean', 'target': 'Mlle.Baptistine', 'value': 3 },
          // { 'source': 'Valjean', 'target': 'Myriel', 'value': 5 },
          // { 'source': 'Marguerite', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Mme.deR', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Isabeau', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Gervais', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Listolier', 'target': 'Tholomyes', 'value': 4 },
          // { 'source': 'Fameuil', 'target': 'Tholomyes', 'value': 4 },
          // { 'source': 'Fameuil', 'target': 'Listolier', 'value': 4 },
          // { 'source': 'Blacheville', 'target': 'Tholomyes', 'value': 4 },
          // { 'source': 'Blacheville', 'target': 'Listolier', 'value': 4 },
          // { 'source': 'Blacheville', 'target': 'Fameuil', 'value': 4 },
          // { 'source': 'Favourite', 'target': 'Tholomyes', 'value': 3 },
          // { 'source': 'Favourite', 'target': 'Listolier', 'value': 3 },
          // { 'source': 'Favourite', 'target': 'Fameuil', 'value': 3 },
          // { 'source': 'Favourite', 'target': 'Blacheville', 'value': 4 },
          // { 'source': 'Dahlia', 'target': 'Tholomyes', 'value': 3 },
          // { 'source': 'Dahlia', 'target': 'Listolier', 'value': 3 },
          // { 'source': 'Dahlia', 'target': 'Fameuil', 'value': 3 },
          // { 'source': 'Dahlia', 'target': 'Blacheville', 'value': 3 },
          // { 'source': 'Dahlia', 'target': 'Favourite', 'value': 5 },
          // { 'source': 'Zephine', 'target': 'Tholomyes', 'value': 3 },
          // { 'source': 'Zephine', 'target': 'Listolier', 'value': 3 },
          // { 'source': 'Zephine', 'target': 'Fameuil', 'value': 3 },
          // { 'source': 'Zephine', 'target': 'Blacheville', 'value': 3 },
          // { 'source': 'Zephine', 'target': 'Favourite', 'value': 4 },
          // { 'source': 'Zephine', 'target': 'Dahlia', 'value': 4 },
          // { 'source': 'Fantine', 'target': 'Tholomyes', 'value': 3 },
          // { 'source': 'Fantine', 'target': 'Listolier', 'value': 3 },
          // { 'source': 'Fantine', 'target': 'Fameuil', 'value': 3 },
          // { 'source': 'Fantine', 'target': 'Blacheville', 'value': 3 },
          // { 'source': 'Fantine', 'target': 'Favourite', 'value': 4 },
          // { 'source': 'Fantine', 'target': 'Dahlia', 'value': 4 },
          // { 'source': 'Fantine', 'target': 'Zephine', 'value': 4 },
          // { 'source': 'Fantine', 'target': 'Marguerite', 'value': 2 },
          // { 'source': 'Fantine', 'target': 'Valjean', 'value': 9 },
          // { 'source': 'Mme.Thenardier', 'target': 'Fantine', 'value': 2 },
          // { 'source': 'Mme.Thenardier', 'target': 'Valjean', 'value': 7 },
          // { 'source': 'Thenardier', 'target': 'Mme.Thenardier', 'value': 13 },
          // { 'source': 'Thenardier', 'target': 'Fantine', 'value': 1 },
          // { 'source': 'Thenardier', 'target': 'Valjean', 'value': 12 },
          // { 'source': 'Cosette', 'target': 'Mme.Thenardier', 'value': 4 },
          // { 'source': 'Cosette', 'target': 'Valjean', 'value': 31 },
          // { 'source': 'Cosette', 'target': 'Tholomyes', 'value': 1 },
          // { 'source': 'Cosette', 'target': 'Thenardier', 'value': 1 },
          // { 'source': 'Javert', 'target': 'Valjean', 'value': 17 },
          // { 'source': 'Javert', 'target': 'Fantine', 'value': 5 },
          // { 'source': 'Javert', 'target': 'Thenardier', 'value': 5 },
          // { 'source': 'Javert', 'target': 'Mme.Thenardier', 'value': 1 },
          // { 'source': 'Javert', 'target': 'Cosette', 'value': 1 },
          // { 'source': 'Fauchelevent', 'target': 'Valjean', 'value': 8 },
          // { 'source': 'Fauchelevent', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Bamatabois', 'target': 'Fantine', 'value': 1 },
          // { 'source': 'Bamatabois', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Bamatabois', 'target': 'Valjean', 'value': 2 },
          // { 'source': 'Perpetue', 'target': 'Fantine', 'value': 1 },
          // { 'source': 'Simplice', 'target': 'Perpetue', 'value': 2 },
          // { 'source': 'Simplice', 'target': 'Valjean', 'value': 3 },
          // { 'source': 'Simplice', 'target': 'Fantine', 'value': 2 },
          // { 'source': 'Simplice', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Scaufflaire', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Woman1', 'target': 'Valjean', 'value': 2 },
          // { 'source': 'Woman1', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Judge', 'target': 'Valjean', 'value': 3 },
          // { 'source': 'Judge', 'target': 'Bamatabois', 'value': 2 },
          // { 'source': 'Champmathieu', 'target': 'Valjean', 'value': 3 },
          // { 'source': 'Champmathieu', 'target': 'Judge', 'value': 3 },
          // { 'source': 'Champmathieu', 'target': 'Bamatabois', 'value': 2 },
          // { 'source': 'Brevet', 'target': 'Judge', 'value': 2 },
          // { 'source': 'Brevet', 'target': 'Champmathieu', 'value': 2 },
          // { 'source': 'Brevet', 'target': 'Valjean', 'value': 2 },
          // { 'source': 'Brevet', 'target': 'Bamatabois', 'value': 1 },
          // { 'source': 'Chenildieu', 'target': 'Judge', 'value': 2 },
          // { 'source': 'Chenildieu', 'target': 'Champmathieu', 'value': 2 },
          // { 'source': 'Chenildieu', 'target': 'Brevet', 'value': 2 },
          // { 'source': 'Chenildieu', 'target': 'Valjean', 'value': 2 },
          // { 'source': 'Chenildieu', 'target': 'Bamatabois', 'value': 1 },
          // { 'source': 'Cochepaille', 'target': 'Judge', 'value': 2 },
          // { 'source': 'Cochepaille', 'target': 'Champmathieu', 'value': 2 },
          // { 'source': 'Cochepaille', 'target': 'Brevet', 'value': 2 },
          // { 'source': 'Cochepaille', 'target': 'Chenildieu', 'value': 2 },
          // { 'source': 'Cochepaille', 'target': 'Valjean', 'value': 2 },
          // { 'source': 'Cochepaille', 'target': 'Bamatabois', 'value': 1 },
          // { 'source': 'Pontmercy', 'target': 'Thenardier', 'value': 1 },
          // { 'source': 'Boulatruelle', 'target': 'Thenardier', 'value': 1 },
          // { 'source': 'Eponine', 'target': 'Mme.Thenardier', 'value': 2 },
          // { 'source': 'Eponine', 'target': 'Thenardier', 'value': 3 },
          // { 'source': 'Anzelma', 'target': 'Eponine', 'value': 2 },
          // { 'source': 'Anzelma', 'target': 'Thenardier', 'value': 2 },
          // { 'source': 'Anzelma', 'target': 'Mme.Thenardier', 'value': 1 },
          // { 'source': 'Woman2', 'target': 'Valjean', 'value': 3 },
          // { 'source': 'Woman2', 'target': 'Cosette', 'value': 1 },
          // { 'source': 'Woman2', 'target': 'Javert', 'value': 1 },
          // { 'source': 'MotherInnocent', 'target': 'Fauchelevent', 'value': 3 },
          // { 'source': 'MotherInnocent', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Gribier', 'target': 'Fauchelevent', 'value': 2 },
          // { 'source': 'Mme.Burgon', 'target': 'Jondrette', 'value': 1 },
          // { 'source': 'Gavroche', 'target': 'Mme.Burgon', 'value': 2 },
          // { 'source': 'Gavroche', 'target': 'Thenardier', 'value': 1 },
          // { 'source': 'Gavroche', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Gavroche', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Gillenormand', 'target': 'Cosette', 'value': 3 },
          // { 'source': 'Gillenormand', 'target': 'Valjean', 'value': 2 },
          // { 'source': 'Magnon', 'target': 'Gillenormand', 'value': 1 },
          // { 'source': 'Magnon', 'target': 'Mme.Thenardier', 'value': 1 },
          // { 'source': 'Mlle.Gillenormand', 'target': 'Gillenormand', 'value': 9 },
          // { 'source': 'Mlle.Gillenormand', 'target': 'Cosette', 'value': 2 },
          // { 'source': 'Mlle.Gillenormand', 'target': 'Valjean', 'value': 2 },
          // { 'source': 'Mme.Pontmercy', 'target': 'Mlle.Gillenormand', 'value': 1 },
          // { 'source': 'Mme.Pontmercy', 'target': 'Pontmercy', 'value': 1 },
          // { 'source': 'Mlle.Vaubois', 'target': 'Mlle.Gillenormand', 'value': 1 },
          // { 'source': 'Lt.Gillenormand', 'target': 'Mlle.Gillenormand', 'value': 2 },
          // { 'source': 'Lt.Gillenormand', 'target': 'Gillenormand', 'value': 1 },
          // { 'source': 'Lt.Gillenormand', 'target': 'Cosette', 'value': 1 },
          // { 'source': 'Marius', 'target': 'Mlle.Gillenormand', 'value': 6 },
          // { 'source': 'Marius', 'target': 'Gillenormand', 'value': 12 },
          // { 'source': 'Marius', 'target': 'Pontmercy', 'value': 1 },
          // { 'source': 'Marius', 'target': 'Lt.Gillenormand', 'value': 1 },
          // { 'source': 'Marius', 'target': 'Cosette', 'value': 21 },
          // { 'source': 'Marius', 'target': 'Valjean', 'value': 19 },
          // { 'source': 'Marius', 'target': 'Tholomyes', 'value': 1 },
          // { 'source': 'Marius', 'target': 'Thenardier', 'value': 2 },
          // { 'source': 'Marius', 'target': 'Eponine', 'value': 5 },
          // { 'source': 'Marius', 'target': 'Gavroche', 'value': 4 },
          // { 'source': 'BaronessT', 'target': 'Gillenormand', 'value': 1 },
          // { 'source': 'BaronessT', 'target': 'Marius', 'value': 1 },
          // { 'source': 'Mabeuf', 'target': 'Marius', 'value': 1 },
          // { 'source': 'Mabeuf', 'target': 'Eponine', 'value': 1 },
          // { 'source': 'Mabeuf', 'target': 'Gavroche', 'value': 1 },
          // { 'source': 'Enjolras', 'target': 'Marius', 'value': 7 },
          // { 'source': 'Enjolras', 'target': 'Gavroche', 'value': 7 },
          // { 'source': 'Enjolras', 'target': 'Javert', 'value': 6 },
          // { 'source': 'Enjolras', 'target': 'Mabeuf', 'value': 1 },
          // { 'source': 'Enjolras', 'target': 'Valjean', 'value': 4 },
          // { 'source': 'Combeferre', 'target': 'Enjolras', 'value': 15 },
          // { 'source': 'Combeferre', 'target': 'Marius', 'value': 5 },
          // { 'source': 'Combeferre', 'target': 'Gavroche', 'value': 6 },
          // { 'source': 'Combeferre', 'target': 'Mabeuf', 'value': 2 },
          // { 'source': 'Prouvaire', 'target': 'Gavroche', 'value': 1 },
          // { 'source': 'Prouvaire', 'target': 'Enjolras', 'value': 4 },
          // { 'source': 'Prouvaire', 'target': 'Combeferre', 'value': 2 },
          // { 'source': 'Feuilly', 'target': 'Gavroche', 'value': 2 },
          // { 'source': 'Feuilly', 'target': 'Enjolras', 'value': 6 },
          // { 'source': 'Feuilly', 'target': 'Prouvaire', 'value': 2 },
          // { 'source': 'Feuilly', 'target': 'Combeferre', 'value': 5 },
          // { 'source': 'Feuilly', 'target': 'Mabeuf', 'value': 1 },
          // { 'source': 'Feuilly', 'target': 'Marius', 'value': 1 },
          // { 'source': 'Courfeyrac', 'target': 'Marius', 'value': 9 },
          // { 'source': 'Courfeyrac', 'target': 'Enjolras', 'value': 17 },
          // { 'source': 'Courfeyrac', 'target': 'Combeferre', 'value': 13 },
          // { 'source': 'Courfeyrac', 'target': 'Gavroche', 'value': 7 },
          // { 'source': 'Courfeyrac', 'target': 'Mabeuf', 'value': 2 },
          // { 'source': 'Courfeyrac', 'target': 'Eponine', 'value': 1 },
          // { 'source': 'Courfeyrac', 'target': 'Feuilly', 'value': 6 },
          // { 'source': 'Courfeyrac', 'target': 'Prouvaire', 'value': 3 },
          // { 'source': 'Bahorel', 'target': 'Combeferre', 'value': 5 },
          // { 'source': 'Bahorel', 'target': 'Gavroche', 'value': 5 },
          // { 'source': 'Bahorel', 'target': 'Courfeyrac', 'value': 6 },
          // { 'source': 'Bahorel', 'target': 'Mabeuf', 'value': 2 },
          // { 'source': 'Bahorel', 'target': 'Enjolras', 'value': 4 },
          // { 'source': 'Bahorel', 'target': 'Feuilly', 'value': 3 },
          // { 'source': 'Bahorel', 'target': 'Prouvaire', 'value': 2 },
          // { 'source': 'Bahorel', 'target': 'Marius', 'value': 1 },
          // { 'source': 'Bossuet', 'target': 'Marius', 'value': 5 },
          // { 'source': 'Bossuet', 'target': 'Courfeyrac', 'value': 12 },
          // { 'source': 'Bossuet', 'target': 'Gavroche', 'value': 5 },
          // { 'source': 'Bossuet', 'target': 'Bahorel', 'value': 4 },
          // { 'source': 'Bossuet', 'target': 'Enjolras', 'value': 10 },
          // { 'source': 'Bossuet', 'target': 'Feuilly', 'value': 6 },
          // { 'source': 'Bossuet', 'target': 'Prouvaire', 'value': 2 },
          // { 'source': 'Bossuet', 'target': 'Combeferre', 'value': 9 },
          // { 'source': 'Bossuet', 'target': 'Mabeuf', 'value': 1 },
          // { 'source': 'Bossuet', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Joly', 'target': 'Bahorel', 'value': 5 },
          // { 'source': 'Joly', 'target': 'Bossuet', 'value': 7 },
          // { 'source': 'Joly', 'target': 'Gavroche', 'value': 3 },
          // { 'source': 'Joly', 'target': 'Courfeyrac', 'value': 5 },
          // { 'source': 'Joly', 'target': 'Enjolras', 'value': 5 },
          // { 'source': 'Joly', 'target': 'Feuilly', 'value': 5 },
          // { 'source': 'Joly', 'target': 'Prouvaire', 'value': 2 },
          // { 'source': 'Joly', 'target': 'Combeferre', 'value': 5 },
          // { 'source': 'Joly', 'target': 'Mabeuf', 'value': 1 },
          // { 'source': 'Joly', 'target': 'Marius', 'value': 2 },
          // { 'source': 'Grantaire', 'target': 'Bossuet', 'value': 3 },
          // { 'source': 'Grantaire', 'target': 'Enjolras', 'value': 3 },
          // { 'source': 'Grantaire', 'target': 'Combeferre', 'value': 1 },
          // { 'source': 'Grantaire', 'target': 'Courfeyrac', 'value': 2 },
          // { 'source': 'Grantaire', 'target': 'Joly', 'value': 2 },
          // { 'source': 'Grantaire', 'target': 'Gavroche', 'value': 1 },
          // { 'source': 'Grantaire', 'target': 'Bahorel', 'value': 1 },
          // { 'source': 'Grantaire', 'target': 'Feuilly', 'value': 1 },
          // { 'source': 'Grantaire', 'target': 'Prouvaire', 'value': 1 },
          // { 'source': 'MotherPlutarch', 'target': 'Mabeuf', 'value': 3 },
          // { 'source': 'Gueulemer', 'target': 'Thenardier', 'value': 5 },
          // { 'source': 'Gueulemer', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Gueulemer', 'target': 'Mme.Thenardier', 'value': 1 },
          // { 'source': 'Gueulemer', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Gueulemer', 'target': 'Gavroche', 'value': 1 },
          // { 'source': 'Gueulemer', 'target': 'Eponine', 'value': 1 },
          // { 'source': 'Babet', 'target': 'Thenardier', 'value': 6 },
          // { 'source': 'Babet', 'target': 'Gueulemer', 'value': 6 },
          // { 'source': 'Babet', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Babet', 'target': 'Mme.Thenardier', 'value': 1 },
          // { 'source': 'Babet', 'target': 'Javert', 'value': 2 },
          // { 'source': 'Babet', 'target': 'Gavroche', 'value': 1 },
          // { 'source': 'Babet', 'target': 'Eponine', 'value': 1 },
          // { 'source': 'Claquesous', 'target': 'Thenardier', 'value': 4 },
          // { 'source': 'Claquesous', 'target': 'Babet', 'value': 4 },
          // { 'source': 'Claquesous', 'target': 'Gueulemer', 'value': 4 },
          // { 'source': 'Claquesous', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Claquesous', 'target': 'Mme.Thenardier', 'value': 1 },
          // { 'source': 'Claquesous', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Claquesous', 'target': 'Eponine', 'value': 1 },
          // { 'source': 'Claquesous', 'target': 'Enjolras', 'value': 1 },
          // { 'source': 'Montparnasse', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Montparnasse', 'target': 'Babet', 'value': 2 },
          // { 'source': 'Montparnasse', 'target': 'Gueulemer', 'value': 2 },
          // { 'source': 'Montparnasse', 'target': 'Claquesous', 'value': 2 },
          // { 'source': 'Montparnasse', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Montparnasse', 'target': 'Gavroche', 'value': 1 },
          // { 'source': 'Montparnasse', 'target': 'Eponine', 'value': 1 },
          // { 'source': 'Montparnasse', 'target': 'Thenardier', 'value': 1 },
          // { 'source': 'Toussaint', 'target': 'Cosette', 'value': 2 },
          // { 'source': 'Toussaint', 'target': 'Javert', 'value': 1 },
          // { 'source': 'Toussaint', 'target': 'Valjean', 'value': 1 },
          // { 'source': 'Child1', 'target': 'Gavroche', 'value': 2 },
          // { 'source': 'Child2', 'target': 'Gavroche', 'value': 2 },
          // { 'source': 'Child2', 'target': 'Child1', 'value': 3 },
          // { 'source': 'Brujon', 'target': 'Babet', 'value': 3 },
          // { 'source': 'Brujon', 'target': 'Gueulemer', 'value': 3 },
          // { 'source': 'Brujon', 'target': 'Thenardier', 'value': 3 },
          // { 'source': 'Brujon', 'target': 'Gavroche', 'value': 1 },
          // { 'source': 'Brujon', 'target': 'Eponine', 'value': 1 },
          // { 'source': 'Brujon', 'target': 'Claquesous', 'value': 1 },
          // { 'source': 'Brujon', 'target': 'Montparnasse', 'value': 1 },
          // { 'source': 'Mme.Hucheloup', 'target': 'Bossuet', 'value': 1 },
          // { 'source': 'Mme.Hucheloup', 'target': 'Joly', 'value': 1 },
          // { 'source': 'Mme.Hucheloup', 'target': 'Grantaire', 'value': 1 },
          // { 'source': 'Mme.Hucheloup', 'target': 'Bahorel', 'value': 1 },
          // { 'source': 'Mme.Hucheloup', 'target': 'Courfeyrac', 'value': 1 },
          // { 'source': 'Mme.Hucheloup', 'target': 'Gavroche', 'value': 1 },
          // { 'source': 'Mme.Hucheloup', 'target': 'Enjolras', 'value': 1 }
        ]
      },
      colorList: ['red', 'rgb(241, 102, 103)', 'rgb(87, 199, 227)', 'yellow', 'orange', 'brown', 'chartreuse', 'violet', 'tan', 'turquoise', 'springgreen'],
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

      let set = new Set()
      data.forEach(item => {
        item.start.id = item.start.partyName
        set.add(item.start) // node
      })
      //  set 转换 数组
      const array = Array.from(set)
      console.log(array)
      // 去重
      let obj = {}
      this.dataList.nodes = array.reduce((cur, next) => {
        obj[next.partyName] ? '' : obj[next.partyName] = true && cur.push(next)
        return cur
      }, [])
      console.log(this.dataList.nodes)
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
        .force('link', d3.forceLink(links).id(d => d.id).distance(120))
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
        .attr('id', d => d.source + '_' + d.type + '_' + d.target)
      
      this.linksName = g.append('g')
        .selectAll('text')
        .data(links)
        .join('text')
        .attr('x', 50)
        .attr('y', 0)
        .style('fill', '#333')
        .style('font-size', 12)
        .style('font-weight', 700)
        .append('textPath')
        .attr('xlink:href', d => '#' + d.source + '_' + d.type + '_' + d.target)
        .text(d => d.type)

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

      this.nodes.append('title').text(d => d.id)

      this.nodesName = g.append('g')
        .selectAll('text')
        .data(nodes)
        .join('text')
        .attr('class', 'node-text')
        .text(function(val) {
          var len = 0
          for (var i = 0; i < val.id.length; i++) {
            var a = val.id.charAt(i)
            if (a.match(/[^\x00-\xff]/ig) != null) {
              len += 2
            } else {
              len += 1
            }
          }
          if (len <= 8) {
            return val.id
          } else {
            const str = val.id.substring(0, 7)
            return str + '...'
          }
        })

      this.simulation.on('tick', () => {
        this.links
        .attr('d', d=> 'M' + d.source.x + ' ' + d.source.y + ' L' +  d.target.x + ' ' + d.target.y)
          // .attr('x1', d => d.source.x)
          // .attr('y1', d => d.source.y)
          // .attr('x2', d => d.target.x)
          // .attr('y2', d => d.target.y)

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
        .attr('id', d => d.source + '_' + d.type + '_' + d.target)
        .merge(this.links)

      this.linksName = this.linksName
        .data(links)
        .enter()
        .append('text')
        .attr('x', 50)
        .attr('y', 0)
        .style('fill', '#333')
        .style('font-size', 12)
        .style('font-weight', 700)
        .append('textPath')
        .attr('xlink:href', d => '#' + d.source + '_' + d.type + '_' + d.target)
        .merge(this.linksName)
        .text(d => d.type)

      this.nodes = this.nodes
        .data(nodes)
        .enter()
        .append('circle')
        .attr('r', r)
        .attr('fill', this.color)
        .merge(this.nodes)
        .on('click', this.circleClk)
        .call(this.drag(this.simulation))

      this.nodes.append('title').text(d => d.id)

      this.nodesName = this.nodesName
        .data(nodes)
        .enter()
        .append('text')
        .attr('class', 'node-text')
        .text(function(val) {
          var len = 0
          for (var i = 0; i < val.id.length; i++) {
            var a = val.id.charAt(i)
            if (a.match(/[^\x00-\xff]/ig) != null) {
              len += 2
            } else {
              len += 1
            }
          }
          if (len <= 8) {
            return val.id
          } else {
            const str = val.id.substring(0, 7)
            return str + '...'
          }
        })
        .merge(this.nodesName)

      //  重新初始化绑定力模型
      this.simulation.nodes(nodes)
      // 修改节点位置和速度的函数
      this.simulation.force('link', d3.forceLink(links).id(d => d.id).distance(120))
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
      axios.get('http://10.20.11.251:8084/szwm/neo/partytocase/selectPartyToCaseByPartyName?partyName=' + items.partyName)
      .then(response => {
        const data = response.data

        let array = []
        data.forEach((item) => {
          item.end.id = item.end.caseName
          item.end.type = item.type
          item.end.group = item.end.group || 2
          array.push(item.end)
        })
        
        array.forEach(item => {
          console.log(item)
          this.dataList.nodes.push(item)
          item.source = items.id
          item.target = item.id
          this.dataList.links.push(item)
        })
        console.log(this.dataList)
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
