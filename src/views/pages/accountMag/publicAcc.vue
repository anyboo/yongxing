<template>
  <div>
    <div id="myChart" :style="{width: '600px', height: '300px'}"></div>
  </div>
</template>

<script>
  export default{
    name:'publicAcc',
    mounted(){
    this.drawLine();
  },
  data(){
    return{}
  },
  methods: {
    drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let myChart = this.$echarts.init(document.getElementById('myChart'))
        // 绘制图表
        myChart.setOption({
            title: { text: '收费统计' },
            tooltip: {},
            xAxis: {
                data: ["桌子","椅子","灯泡","门","柜子","窗户"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        });
    }
  }
    
    
  }
</script>

<style>
  
</style>