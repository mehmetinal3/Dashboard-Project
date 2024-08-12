<template>
  <div class="container">
    <div class="row row-1">
      <div v-for="(squareboxitems, index) in squareboxitems" :key="index" :class="`box box-${index + 1}`">
        <div class="small-box">
          <div class="up">
            <div class="left">
              <i :class="squareboxitems.bigicon"></i>
              <div class="badge">
                <i :class="squareboxitems.smallicon"></i>
                <strong>{{ squareboxitems.percent }}</strong>
              </div>
            </div>
            <div class="right">
              <div class="right-up">
                {{ squareboxitems.title }}
              </div>
                <h2 class="right-down">{{ squareboxitems.number }}</h2>
            </div>
          </div>
          <div class="down" v-html="squareboxitems.image"></div>
        </div>
      </div>
    </div>
    <div class="row row-2">
      <div class="box box-5">
        <img src="../assets/statistics-canvas.jpeg">
      </div>
    </div>
    <div class="row row-3">
      <div class="box box-6">
        <div class="progress-box">
          <div class="on-progress-box">
              <LongUp :title="title1" :date="date1" defaultSelected="Month"/>
          </div>
          <div class="under-progress-box">
            <table>
              <tr><th v-for="progressunderboxitem in progressunderboxitems" :key="progressunderboxitem.tabletitle">{{ progressunderboxitem.tabletitle }}</th></tr>
              <tr v-for="(progressunderboxitem, index) in progressunderboxitems" :key="progressunderboxitem.tabletitle">
                  <td class="td-left"><span :class="`${progressunderboxitem.animation}`" :style="{ backgroundColor: pulseColor(index) }"></span></td>
                  <td>{{ progressunderboxitem.firstname }}</td>
                  <td>{{ progressunderboxitem.lastname }}</td>
                  <td v-html="progressunderboxitem.activity"></td>
                  <td style="min-width: 195px;">
                      <div class="progress-bar">
                        <div class="progress-bar-outer">
                          <div class="progress-bar-inner" :style="{width: progressunderboxitem.barwidth, backgroundColor: progressunderboxitem.barcolor}"></div>
                        </div>
                        <div class="progress-text" style="font-size: 14.4px;"><span v-html="progressunderboxitem.progresstext"></span></div>
                      </div>
                  </td>
                </tr>
            </table>
          </div>
        </div>
      </div>
      <div class="box box-7">
        <img src="../assets/canvas-2.jpeg">
      </div>
    </div>
    <div class="row row-4">
      <div class="box box-8">
        <div class="report-box">
          <div class="on-report-box">
            <LongUp :title="title2" :date="date2" defaultSelected="Week"/>
          </div>
          <div class="under-report-box">
            <div v-for="(reportunderboxitem, index) in reportunderboxitems" :key="index" class="under-report-box-2">
              <h4>{{ reportunderboxitem.title }}</h4>
              <div class="progress-bar">
                <div class="progress-bar-outer">
                  <div class="progress-bar-inner" :style="{ width: reportunderboxitem.width, backgroundColor: reportunderboxitem.background }"></div>
                </div>
                <div :class="`progress-text icon-${index}`"><span><i v-html="reportunderboxitem.baricon" class="el-icon"></i></span></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, onUpdated } from "vue";
import LongUp from "./LongUp.vue";
import { squareboxitems , progressunderboxitems, reportunderboxitems } from '../data/boxitems'
// import '../assets/css/Screengrid/grid.css'
import '../assets/css/Screengrid/squarebox.css'
import '../assets/css/Screengrid/progress.css'
import '../assets/css/Screengrid/reportbox.css'

export default defineComponent({
  name: 'ScreenField',
  components: {
    LongUp
  },
  setup() {

    const pulseColors = [
      '#3B82F6',
      '#FDE047',
      '#4ADE80',
      '#F97316',
      '#D1D5DB'
    ];

    function pulseColor(index: number): string {
      const colorIndex = index % pulseColors.length;
      return pulseColors[colorIndex];
    }

    function applyAfterStyles() {
      const spans = document.querySelectorAll('.td-left span');
      spans.forEach(span => {
        const htmlElement = span as HTMLElement; // Tip dönüşümü
        const backgroundColor = getComputedStyle(htmlElement).backgroundColor;
        htmlElement.style.setProperty('--after-bg-color', backgroundColor);
      });
    }

    onMounted(() => {
      applyAfterStyles();
    });

    onUpdated(() => {
      applyAfterStyles();
    });

    squareboxitems;
    progressunderboxitems;
    reportunderboxitems;

    const title1 = ref('Progress');
    const title2 = ref('Report');

    const date1 = ref('This month');
    const date2 = ref('This week');

    return { squareboxitems, progressunderboxitems, reportunderboxitems, title1, title2, date1, date2, pulseColor }
  },
});
</script>

<style>
@media (max-width: 1200px) {
  .row-1 {
    flex-wrap: wrap;
    height: 430px; 
  }

  .row-1 .box{
    flex: 1 1 calc(50% - 30px); 
    box-sizing: border-box; 
  }
  .row-1 .box-1,.box-2{
    margin-bottom: 15px;
  }
}

@media (max-width: 800px) {
  .row-1 {
    flex-wrap: wrap;
    height: 430px; 
  }

  .row-1 .box{
    flex: 1 1 calc(50% - 30px); 
    box-sizing: border-box; 
  }
}
</style>