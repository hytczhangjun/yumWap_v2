
<template>
  <div class="RepairDetail">
    <div class="title">
      <div class="back" @click="goBack"><返回</div>
      <span>报警数量</span>
    </div>
    <div class="sort-wrapper">
      <div class="sort" @click="handleSort">
        <div class="triangle-down"></div>
        <span class="label">筛选：</span>
        <span class="">{{sortName}}</span>
      </div>
    </div>
    <mt-actionsheet :actions="actions" v-model="sheetVisible"></mt-actionsheet>
    <type-fanChart :list="typeAnalysisList" :chartInfo="typeChartInfo" :title="typeTile" :pageType="typePageType"></type-fanChart>
    <type-fanChart :list="levelList" :chartInfo="levelChartInfo" :title="levelTitle" :pageType="levelPageType"></type-fanChart>
    <trend-analysis :yAxisData="yAxis"></trend-analysis>
    <store-ranking :superList="superList" :totalList="totalList" :type="rankType"></store-ranking>
    <y-footer :nav="footerNav"></y-footer>
  </div>
</template>
<script>
  import TypeFanChart from '@/components/TypeFanChart'
  import TrendAnalysis from '@/components/TrendAnalysis'
  import StoreRanking from '@/components/StoreRanking'
  import YFooter from '@/components/Footer'
  export default {
    data () {
      return {
        sortName: '过去一年',
        sheetVisible: false,
        actions: [],
        typePageType: 2,
        typeTile: '报警类型',
        levelTitle: '报警级别',
        levelPageType: 1,
        typeChartInfo: {
          title: '全月总计',
          count: 240
        },
        levelChartInfo: {
          title: '全月总计',
          count: 45
        },
        typeAnalysisList: [
          {
            name: '冷链系统:',
            value: '16.8'
          },
          {
            name: '电气系统:',
            value: '4.7'
          },
          {
            name: '空调系统:',
            value: '2.3'
          },
          {
            name: '照明系统:',
            value: '1.6'
          }
        ],
        levelList: [
          {
            name: '特级报警:',
            value: '4'
          },
          {
            name: '高级报警:',
            value: '16'
          },
          {
            name: '中级报警:',
            value: '16'
          },
          {
            name: '低级报警:',
            value: '18'
          }
        ],
        superList: ['浦东一店', '浦东二店', '杨浦二店', '徐汇一店', '静安三店'],
        totalList: ['浦东一店', '浦东二店', '杨浦二店', '徐汇一店', '静安三店'],
        footerNav: 0,
        yAxis: {
          name: '个数',
          data: [50, 70, 80, 100, 150, 120, 90, 150, 180, 100, 80, 40]
        },
        rankType: 1
      }
    },
    mounted () {
      this.actions = [
        {
          name: '过去一年',
          method: this.selectSort
        },
        {
          name: '过去两年',
          method: this.selectSort
        }
      ]
    },
    components: {
      TypeFanChart,
      TrendAnalysis,
      StoreRanking,
      YFooter
    },
    methods: {
      goBack () {
        this.$router.go(-1)
      },
      handleSort () {
        this.sheetVisible = true
      },
      selectSort (val) {
        this.sortName = val.name
      }
    }
  }
</script>
<style lang="scss">
  .RepairDetail {
    background: #F4F8FB;
    width: 100%;
    min-height: 100%;
    height: auto;
    padding-bottom: 0.59rem;

    .title {
      position: relative;
      font-size: 18px;
      color: #000000;
      padding: 0.12rem 0;
      text-align: center;

      .back {
        font-size: 14px;
        color: #688BA6;
        letter-spacing: 0;
        margin-left: 0.1rem;
        position: absolute;
        left: 0.1rem;
        line-height: 28px;
      }
    }

    .sort-wrapper {
      margin: 0.1rem 0;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 0;

      .triangle-down {
        width: 0;
        height: 0;
        border-left: 4px solid transparent;
        border-right: 4px solid transparent;
        border-top: 8px solid #D0D0D0;
        display: inline-block;
        margin-right: 5px;
      }

      span {
        font-size: 12px;
        color: #707070;
      }
    }
  }
</style>
