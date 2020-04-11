<template>
  <div style="display: -webkit-box;">
    <div ref="echart1" style="width: 600px;height: 500px;-webkit-box-flex:1;" />
    <div ref="echart2" style="width: 600px;height: 500px;-webkit-box-flex:1;padding-left: 10px" />
  </div>
</template>
<script>
import echarts from 'echarts'
export default {
  name: 'Index',
  mounted() {
    this.showEchart1()
    this.showEchart2()
  },
  methods: {
    showEchart1() {
      const echart1 = echarts.init(this.$refs.echart1)
      const myColor = ['#eb2100', '#eb3600', '#d0570e', '#d0a00e', '#34da62', '#00e9db', '#00c0e9', '#0096f3', '#33CCFF', '#33FFCC']
      const option = {
        backgroundColor: '#0e2147',
        grid: {
          left: '11%',
          top: '12%',
          right: '0%',
          bottom: '8%',
          containLabel: true
        },
        xAxis: [{
          show: false
        }],
        yAxis: [{
          axisTick: 'none',
          axisLine: 'none',
          offset: '27',
          axisLabel: {
            textStyle: {
              color: '#ffffff',
              fontSize: '16'
            }
          },
          data: ['南昌转运中心', '广州转运中心', '杭州转运中心', '宁夏转运中心', '兰州转运中心', '南宁转运中心', '长沙转运中心', '武汉转运中心', '合肥转运中心', '贵州转运中心']
        }, {
          axisTick: 'none',
          axisLine: 'none',
          axisLabel: {
            textStyle: {
              color: '#ffffff',
              fontSize: '16'
            }
          },
          data: ['10', '9', '8', '7', '6', '5', '4', '3', '2', '1']
        }, {
          name: '分拨延误TOP 10',
          nameTextStyle: {
            color: '#ffffff',
            fontSize: '16'
          },
          axisLine: {
            lineStyle: {
              color: 'rgba(0,0,0,0)'
            }
          },
          data: []
        }],
        series: [{
          name: '条',
          type: 'bar',
          yAxisIndex: 0,
          data: [4, 13, 25, 29, 38, 44, 50, 52, 60, 72],
          label: {
            normal: {
              show: true,
              position: 'right',
              textStyle: {
                color: '#ffffff',
                fontSize: '16'
              }
            }
          },
          barWidth: 12,
          itemStyle: {
            normal: {
              color: function(params) {
                var num = myColor.length
                return myColor[params.dataIndex % num]
              }
            }
          },
          z: 2
        }, {
          name: '白框',
          type: 'bar',
          yAxisIndex: 1,
          barGap: '-100%',
          data: [99, 99.5, 99.5, 99.5, 99.5, 99.5, 99.5, 99.5, 99.5, 99.5],
          barWidth: 20,
          itemStyle: {
            normal: {
              color: '#0e2147',
              barBorderRadius: 5
            }
          },
          z: 1
        }, {
          name: '外框',
          type: 'bar',
          yAxisIndex: 2,
          barGap: '-100%',
          data: [100, 100, 100, 100, 100, 100, 100, 100, 100, 100],
          barWidth: 24,
          itemStyle: {
            normal: {
              color: function(params) {
                var num = myColor.length
                return myColor[params.dataIndex % num]
              },
              barBorderRadius: 5
            }
          },
          z: 0
        },
        {
          name: '外圆',
          type: 'scatter',
          hoverAnimation: false,
          data: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
          yAxisIndex: 2,
          symbolSize: 35,
          itemStyle: {
            normal: {
              color: function(params) {
                var num = myColor.length
                return myColor[params.dataIndex % num]
              },
              opacity: 1
            }
          },
          z: 2
        }
        ]
      }
      echart1.setOption(option)
    },
    showEchart2() {
      const option = {
        title: {
          text: '2019年销售水量和主营业务收入对比',
          textStyle: {
            align: 'center',
            color: '#fff',
            fontSize: 20
          },
          top: '3%',
          left: '10%'
        },
        backgroundColor: '#0f375f',
        grid: {
          top: '25%',
          bottom: '10%'// 也可设置left和right设置距离来控制图表的大小
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow',
            label: {
              show: true
            }
          }
        },
        legend: {
          data: ['销售水量', '主营业务'],
          top: '15%',
          textStyle: {
            color: '#ffffff'
          }
        },
        xAxis: {
          data: [
            '当年完成水量',
            '去年同期水量',
            '滚动目标值水量',
            '全年目标值水量',
            '当年完成金额',
            '去年同期金额',
            '滚动目标金额',
            '全年目标值'

          ],
          axisLine: {
            show: true, // 隐藏X轴轴线
            lineStyle: {
              color: '#01FCE3'
            }
          },
          axisTick: {
            show: true // 隐藏X轴刻度
          },
          axisLabel: {
            show: true,
            textStyle: {
              color: '#ebf8ac' // X轴文字颜色
            }
          }

        },
        yAxis: [{
          type: 'value',
          name: '亿元',
          nameTextStyle: {
            color: '#ebf8ac'
          },
          splitLine: {
            show: false
          },
          axisTick: {
            show: true
          },
          axisLine: {
            show: true,
            lineStyle: {
              color: '#FFFFFF'
            }
          },
          axisLabel: {
            show: true,
            textStyle: {
              color: '#ebf8ac'
            }
          }

        },
        {
          type: 'value',
          name: '同比',
          nameTextStyle: {
            color: '#ebf8ac'
          },
          position: 'right',
          splitLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLine: {
            show: false
          },
          axisLabel: {
            show: true,
            formatter: '{value} %', // 右侧Y轴文字显示
            textStyle: {
              color: '#ebf8ac'
            }
          }
        },
        {
          type: 'value',
          gridIndex: 0,
          min: 50,
          max: 100,
          splitNumber: 8,
          splitLine: {
            show: false
          },
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            show: false
          },
          splitArea: {
            show: true,
            areaStyle: {
              color: ['rgba(250,250,250,0.0)', 'rgba(250,250,250,0.05)']
            }
          }
        }
        ],
        series: [{
          name: '销售水量',
          type: 'line',
          yAxisIndex: 1, // 使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用
          smooth: true, // 平滑曲线显示
          showAllSymbol: true, // 显示所有图形。
          symbol: 'circle', // 标记的图形为实心圆
          symbolSize: 10, // 标记的大小
          itemStyle: {
            // 折线拐点标志的样式
            color: '#058cff'
          },
          lineStyle: {
            color: '#058cff'
          },
          areaStyle: {
            color: 'rgba(5,140,255, 0.2)'
          },
          data: [4.2, 3.8, 4.8, 3.5, 2.9, 2.8, 3, 5]
        },
        {
          name: '主营业务',
          type: 'bar',
          barWidth: 15,
          itemStyle: {
            normal: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                offset: 0,
                color: '#00FFE3'
              },
              {
                offset: 1,
                color: '#4693EC'
              }
              ])
            }
          },
          data: [4.2, 3.8, 4.8, 3.5, 2.9, 2.8, 3, 5]
        }]
      }
      const myCharts = echarts.init(this.$refs.echart2)
      myCharts.setOption(option)
    }
  }
}
</script>

<style scoped>

</style>
