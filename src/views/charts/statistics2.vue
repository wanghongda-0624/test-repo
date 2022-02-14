/**
* 图表界面
*/ 
<template class="template">
  <div class="stbox" >
   <el-row :gutter="20">
     <el-col :span="5">
    <div class="grid-content bg-purple">
      <el-button type="text" class="azurecost">28.1K</el-button>
      <el-header class="azuretotal">Total Cost</el-header>
      <div class="whitebox" @click="azuresso()"><img src="../../assets/img/Azure.svg" class="azureimg" width="70px">
      </img></div>
    </div>
    </el-col>
  <el-col :span="5">
    <div class="grid-content bg-purple2">
      <el-button type="text" class="alicost">28.1K</el-button>
      <el-header class="alitotal">Total Cost</el-header>
      <div class="whitebox2"><img src="../../assets/img/阿里云.svg" class="aliimg" width="80px">
      </img></div>
    </div>
    </el-col>
  <el-col :span="5"><div class="grid-content bg-purple3">
      <el-button type="text" class="hwcost">28.1K</el-button>
      <el-header class="hwtotal">Total Cost</el-header>
      <div class="whitebox3"><img src="../../assets/img/华为1.svg" class="hwimg" width="85px" height="40px">
      </img></div>
    </div></el-col>
  <el-col :span="5"><div class="grid-content bg-purple4">
    <el-button type="text" class="txcost">28.1K</el-button>
      <el-header class="txtotal">Total Cost</el-header>
      <div class="whitebox4"><img src="../../assets/img/tx.svg" class="tximg" width="85px" height="40px">
      </img></div>
    </div></el-col>
    <div style="margin-top:0px">
  </div>
  </el-row>
  <div class="st-gbox">
          <div class="cavasbox" ref="SUMEchart"></div>
  </div>
  <el-row :gutter="20">
      <el-col :span="10" class="text-c">
        <div class="st-gbox2">
          <div class="cavasbox" ref="ClickEchart"></div>
        </div>
      </el-col>
      <el-col :span="10" class="text-c">
        <div class="st-gbox3">
          <div class="cavasbox" ref="payEchart"></div>
        </div>
      </el-col>
    </el-row>
  <div class="rightnav">
    <p class="p1">Start Date</p>
    <el-date-picker
              type="date"
              placeholder="start date"
              style="width: 80% ; margin-left:10%"
            ></el-date-picker>
    <p class="p2">End Date</p>
    <el-date-picker
              type="date"
              placeholder="end date"
              style="width: 80% ; margin-left:10%"
            ></el-date-picker>
    <p class="p3">Category</p>
    <el-radio-group v-model="radio" class="group">
      <el-radio :label="3" class="r1">Compute</el-radio>
      <el-radio :label="6" class="r2">Storage</el-radio>
      <el-radio :label="9" class="r3">Network</el-radio>
    </el-radio-group>
    <img class="bot" src= "../../assets/img/sticky-icon.gif" />
  </div>
  </div>
</template>
<script type="text/ecmascript-6">
import Chart from "echarts";
export default {
  name: "login",
  data() {
    return {
      //定义loading默认为false
      logining: false,
      // 记住密码
      rememberpwd: false,
      ruleForm: {
        //username和password默认为空
        username: "",
        password: "",
        code: "",
        randomStr: "",
        codeimg: "",
      },
      //radio group
      radio: 3,
      //rules前端验证
      rules: {
        username: [{ required: true, message: "请输入账号", trigger: "blur" }],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }],
        code: [{ required: true, message: "请输入验证码", trigger: "blur" }],
      },
      //pie
      payoption:{
  title: {
    text: 'Resource Cost',
    textStyle:{
        color: '#515151',
        fontStyle: 'normal',
        fontSize:'20px'
    },
    // subtext: 'Fake Data',
    textAlign: 'left'
  },
  tooltip: {
    trigger: 'item'
  },
  legend: {
    show: false,
    orient: 'vertical',
    left: 'left'
  },
  series: [
    {
      name: 'Resource Type',
      type: 'pie',
      radius: '50%',
      data: [
        { value: 1048, name: 'ECS' },
        { value: 735, name: 'Database' },
        { value: 580, name: 'Storage' },
        { value: 484, name: 'Network' },
        { value: 300, name: 'Container' }
      ],
      emphasis: {
        itemStyle: {
          shadowBlur: 10,
          shadowOffsetX: 0,
          shadowColor: 'rgba(0, 0, 0, 0.5)'
        }
      }
    }
  ]
},
      //  销售总金额
      SUMoption: {
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}月 : {c}",
        },
        legend: {
          data: [
            {
              name: "Total Cost",
              icon: "rect",
            },
          ],
          top: 1,
          left: 1,
          itemGap: 10,
          itemWidth: 12,
          itemHeight: 12,
          textStyle: {
            fontSize: 12,
            color: "#323232",
          },
        },
        grid: {
          left: 50,
          right: 10,
          top: 30,
          bottom: 30,
          borderWidth: 1,
        },
        xAxis: {
          type: "category",
          data: ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12"],
          axisLine: {
            lineStyle: {
              color: "#999999",
              width: 1,
            },
          },
          axisLabel: {
            margin: 14,
            height: 70,
            interval: 0,
            textStyle: {
              fontSize: 10,
              color: "#999999",
            },
          },
        },
        yAxis: {
          type: "value",
          axisLine: {
            lineStyle: {
              color: "#999999",
              width: 1,
            },
          },
          axisLabel: {
            margin: 14,
            textStyle: {
              fontSize: 10,
              color: "#999999",
            },
          },
        },
        series: [
          {
            name: "Total Cost",
            //   type: 'bar',
            type: "line",
            barGap: 0,
            data: [
              50000, 70000, 80000, 40000, 50000, 30000, 40000, 60000, 50000,
              40000, 60000, 40000,
            ],
            barWidth: 10,
            itemStyle: {
              color: "#108ff9",
            },
          },
        ],
      },

      //  总点击量
      Clickoption: {
        tooltip: {
          trigger: 'item',
          formatter: "{a} <br/>{b}月 : {c}"
        },
        legend: {
          data: [{
            name: 'Application Cost',
            icon: 'rect'
          }],
          top: 1,
          left: 1,
          itemGap: 10,
          itemWidth: 12,
          itemHeight: 12,
          textStyle: {
            fontSize: 12,
            color: "#323232"
          }
        },
        grid: {
          left: 50,
          right: 10,
          top: 30,
          bottom: 30,
          borderWidth: 1
        },
        xAxis: {
          type: 'category',
          data: ['App1', 'App2', 'App3', 'App4', 'App5', 'App6', 'App7', 'App8'],
          axisLine: {
            lineStyle: {
              color: "#999999",
              width: 1
            }
          },
          axisLabel: {
            margin: 14,
            height: 70,
            interval: 0,
            textStyle: {
              fontSize: 10,
              color: "#999999"
            }
          }
        },
        yAxis: {
          type: 'value',
          axisLine: {
            lineStyle: {
              color: "#999999",
              width: 1
            }
          },
          axisLabel: {
            margin: 14,
            textStyle: {
              fontSize: 10,
              color: "#999999"
            }
          }
        },
        series: [{
          name: 'Application Cost',
          type: 'bar',
          barGap: 0,
          data: [50000, 10000, 80000, 30000, 50000, 60000, 40000, 80000],
          barWidth: 10,
          itemStyle: {
            color: "#48cefd"
          }
        }]
      },
    };
  },
  // 创建完毕状态(里面是操作)
  created() {
    this.$store.state.showright = false;
  },

  // 里面的函数只有调用才会执行
  methods: {
    // 获取用户名密码
    azuresso() {
      console.log("1234");
      window.open("https://portal.azure.cn");
    },
    getSUM() {
      this.chart = Chart.init(this.$refs.SUMEchart);
      this.chart.setOption(this.SUMoption);
    },
    getpay() {
      this.chart = Chart.init(this.$refs.payEchart)
      this.chart.setOption(this.payoption)
    },
    getClick() {
      this.chart = Chart.init(this.$refs.ClickEchart)
      this.chart.setOption(this.Clickoption)
    },
  },
  mounted() {
    this.getSUM();
    this.getpay();
    this.getClick();
  },
};
</script>
<style>
.stbox {
  display: inline-block;
  width: 100%;
  height: 98%;
  box-sizing: border-box;
  white-space: nowrap;
}

.el-row {
  margin-bottom: 20px;
  &:last-child {
    margin-bottom: 0;
  }
}
.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #d04a02;
}
.bg-purple2 {
  background: #db536a;
}
.bg-purple3 {
  background: #eb8c00;
}
.bg-purple4 {
  background: #e0301e;
}
.bg-purple5 {
  background: #fff;
  /* position: absolute;
    top:300px; */
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 4px;
  min-height: 85px;
}
.whitebox {
  border-radius: 4px;
  min-height: 50px;
  width: 90px;
  background-color: #fff;
  position: absolute;
  top: 15px;
  left: 25px;
}
.azureimg {
  padding-top: 10px;
  padding-left: 5px;
}
.azurecost {
  position: absolute;
  top: 8px;
  left: 125px;
}
.azurecost.el-button--text {
  color: #fff;
  font-size: 25px;
}
.azuretotal {
  position: absolute;
  top: 55px;
  left: 105px;
  font-size: 15px;
  color: #fff;
}

.whitebox2 {
  border-radius: 4px;
  min-height: 50px;
  width: 90px;
  background-color: #fff;
  position: absolute;
  top: 15px;
  left: 23.5%;
}
.aliimg {
  padding-top: 10px;
  padding-left: 5px;
}
.alicost {
  position: absolute;
  top: 8px;
  left: 33%;
}
.alicost.el-button--text {
  color: #fff;
  font-size: 25px;
}
.alitotal {
  position: absolute;
  top: 55px;
  left: 31%;
  font-size: 15px;
  color: #fff;
}
.grid-content2 {
  border-radius: 4px;
  min-height: 50px;
}

.whitebox3 {
  border-radius: 4px;
  min-height: 50px;
  width: 90px;
  background-color: #fff;
  position: absolute;
  top: 15px;
  left: 44.5%;
}
.hwimg {
  padding-top: 8px;
  padding-left: 5px;
}
.hwcost {
  position: absolute;
  top: 8px;
  left: 54%;
}
.hwcost.el-button--text {
  color: #fff;
  font-size: 25px;
}
.hwtotal {
  position: absolute;
  top: 55px;
  left: 52%;
  font-size: 15px;
  color: #fff;
}

.whitebox4 {
  border-radius: 4px;
  min-height: 50px;
  width: 90px;
  background-color: #fff;
  position: absolute;
  top: 15px;
  left: 65%;
}
.tximg {
  padding-top: 5px;
  padding-left: 5px;
}
.txcost {
  position: absolute;
  top: 8px;
  left: 75%;
}
.txcost.el-button--text {
  color: #fff;
  font-size: 25px;
}
.txtotal {
  position: absolute;
  top: 55px;
  left: 73%;
  font-size: 15px;
  color: #fff;
}
.el-header.index-header {
  border-left: 0px;
}

.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
.template {
  background-color: #fff;
}
.rightnav {
  background-color: #fff;
  width: 12%;
  height: 90%;
  position: absolute;
  left: 88%;
  top: 9.2%;
}
.p1 {
  margin-left: 14%;
  margin-top: 30%;
}
.p2 {
  margin-left: 14%;
  margin-top: 20%;
}
.p3 {
  margin-left: 14%;
  margin-top: 20%;
}
.r1{
  margin-left: 14%;
  margin-top: 1%;
}
.r2{
  margin-left: 14%;
  margin-top: 10%;
}
.r3{
  margin-left: 14%;
  margin-top: 10%;
}
.group
{
    display: flex;
    flex-direction: column;
}
.st-gbox {
  background-color: #fff;
  margin-top: 20px;
  border-radius: 5px;
  height: 30vh;
  box-sizing: border-box;
  padding: 10px;
  width: 83%;
}
.st-gbox2{
  background-color: #fff;
  margin-top: 20px;
  border-radius: 5px;
  height: 30vh;
  box-sizing: border-box;
  /* padding: 10px; */
  width: 100%;
}
.st-gbox3{
  background-color: #fff;
  margin-top: 20px;
  border-radius: 5px;
  height: 30vh;
  box-sizing: border-box;
  /* padding: 10px; */
  width: 100%;
  padding-left: 1%;
}
.cavasbox {
  box-sizing: border-box;
  width: 100%;
  height: 80%;
}
.text-c {
  text-align: center;
}
.bot{
  margin-left: 20%;
  margin-top: 30%;
}
</style>