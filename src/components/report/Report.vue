<template>
  <div>
    <!-- 面包屑导航区域 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>数据统计</el-breadcrumb-item>
      <el-breadcrumb-item>数据报表</el-breadcrumb-item>
    </el-breadcrumb>

    <el-card>
      <div id="main" style="width: 600px; height: 400px"></div>
    </el-card>
  </div>
</template>

<script>
//导入echarts
import * as echarts from "echarts";
import _ from 'lodash'
export default {
  data() {
    return {
      options: {
        title: {
          text: '用户来源'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
            label: {
              backgroundColor: '#E9EEF3'
            }
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            boundaryGap: false
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ]
      }
    };
  },
  created() {

  },
async mounted() {
    //初始化echart实例
    var myChart = echarts.init(document.getElementById("main"));
    const{data:res}=await this.$http.get('reports/type/1')
    if(res.meta.status!=200){
        return this.$message.error('获取折线图数据失败！')
    }
    //准备数据和配置项
    const result=_.merge(res.data,this.options)
    //展示数据
    myChart.setOption(result)
  },
  methods: {},
};
</script>

<style lang='less' scoped>
</style>