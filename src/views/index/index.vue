<template>
  <div>
  <!--后台主页-->
    <el-row :gutter="20">
    <!--第一排四个小card-->
     <el-col :span="6" v-for="item in main_data.IndexHeader" :key="item.id" class="h1_card">
       <router-link to="">
        <el-card class="box-card" shadow="hover">
          <div style="display:inline-flex;">
            <i :class="item.icon" :style="item.style"></i>
            <div class="title">
              <p style="margin:0px;">{{item.num}}</p>
              <small style="font-size:.25rem">{{item.cass}}</small>
            </div>
          </div>
        </el-card>
       </router-link>
      </el-col>
    </el-row>
    <!--左边1列-->
    <el-col :span="12" class="indexLeft">
      <el-card class="box-card" shadow="hover" style="height:190px;margin-bottom:30px;">
         <div slot="header" class="clearfix">
           <span>{{main_data.LeftCard.top.title}}</span>
            <el-button style="float: right; padding: 3px 0" type="text">{{main_data.LeftCard.top.subtitle}}</el-button>
         </div>
        <el-row :gutter="10" style="display:flex">
          <el-col :xs="24" :sm="4" :md="4" :lg="4" :xl="4" 
          v-for="item in main_data.LeftCard.top.data" 
          :key="item.id" >
            <div class="grid-content bg-purple" >
              <button class="btn">
                <h4>{{item.num}}</h4>
                <small>{{item.state}}</small>
              </button>
            </div>
          </el-col>
        </el-row>
      </el-card>
      <el-card class="box-card" shadow="hover" style="height:190px;width:100%">
         <div slot="header" class="clearfix">
           <span>{{main_data.LeftCard.bottom.title}}</span>
            <el-button style="float: right; padding: 3px 0" type="text">{{main_data.LeftCard.bottom.subtitle}}</el-button>
         </div>
        <el-row :gutter="10">
          <el-col :xs="2" :sm="4" :md="4" :lg="4" :xl="4" v-for="item in main_data.LeftCard.bottom.data" :key="item.id">
            <div class="grid-content bg-purple">
              <button class="btn">
                <h4>{{item.num}}</h4>
                <small>{{item.state}}</small>
              </button>
            </div>
          </el-col>
        </el-row>
      </el-card>
    </el-col>
    <!--右边图表-->
    <el-col :span="12" style="padding:1.2%">
      <el-card class="box-card" shadow="hover" style="height:420px;width:100%">
         <div slot="header" class="clearfix">
           <span>订单总数统计</span>
            <el-button style="float: right; padding: 3px 0" type="text">订单数量</el-button>
            </div>
            <div ref="gong" style="width:100%;height:270px;">
          </div>
      </el-card>
    </el-col>
    <!--最底层的图表-->
    <el-row :gutter="10">
  <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="padding:1%">
    <!--底部左边卡片-->
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>卡片名称</span>
          <el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>
        </div>
      111111111111111111
      </el-card>
  </el-col>
  <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="padding:1%">
    <!--底部左边卡片-->
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>单品销量排名</span>
          <el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>
        </div>
          <el-table
    :data="main_data.tableRight"
    height="250"
    border
    style="width: 100%">
    <el-table-column
      prop="date"
      label="#"
      width="100">
    </el-table-column>
    <el-table-column
      prop="name"
      label="商品信息"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="销量">
    </el-table-column>
  </el-table>
      </el-card>
  </el-col>
</el-row>
  </div>
</template>
<script>
import common from "@/common/mixins/common.js";
import echarts from "echarts";
export default {
  mixins:[common],
  name:"index_index",
  data () {
    return {
        main_data:{
          LeftCard:{
            top:{
              title:'店铺及商品提示',
              subtitle:'你需要及时补充的商品',
              data:[
                {id:1, state:'缺货',num:64},
                {id:2, state:'即将缺货',num:112},
                {id:3, state:'出售中',num:36},
                {id:4, state:'出售中',num:32}
                ]
            },
            bottom:{
                title:'交易提示',
              subtitle:'你需要立即处理的交易订单',
              data:[
                {id:1, state:'缺货',num:64},
                {id:2, state:'即将缺货',num:112},
                {id:3, state:'出售中',num:36},
                {id:4, state:'即将缺货',num:112},
                {id:5, state:'出售中',num:36},
                {id:6, state:'出售中',num:32}
                ]
            }
          },
          IndexHeader:[
          {
            id: 1, icon: 'el-icon-user-solid',
            cass:'关注人数(个)', num:'30',
            style:'margin-right:.5rem;background-color:#6B238E;width:50px;height:40px;text-align:center;    line-height:40px;color:#fff;'
          },
          {
          id: 2, icon: 'el-icon-s-order',
          cass:'订单总数(笔)', num:'120',
          style:'margin-right:.5rem;background-color:#7093DB;width:50px;height:40px;text-align:center;    line-height:40px;color:#fff;'},
          {
          id: 3, icon: 'el-icon-s-ticket',
          cass:'今日订单总金额(元)', num:'4183',
          style:'margin-right:.5rem;background-color:#00009C;width:50px;height:40px;text-align:center;    line-height:40px;color:#fff;'
          },
          {
          id: 4, icon: 'el-icon-s-management',
          cass:'本月销量(笔)', num:'100',
          style:'margin-right:.5rem;background-color:#7F00FF;    width:50px;height:40px;text-align:center;    line-height:40px;color:#fff;'
          }
      ],
       tableRight: [{
          date: '1',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '3',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '4',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '5',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '6',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '7',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }],
        },
    }
  },
mounted(){
    //画统计图
    this.line()
  },
  methods:{
    line(){
      console.log(this.$refs.gong);
      let myChart = echarts.init(this.$refs.gong);
      var option = {
    tooltip : {
        trigger: 'axis',
        axisPointer: {
            type: 'cross',
            label: {
                backgroundColor: '#6a7985'
            }
        }
    },
    legend: {
        data:['邮件营销','联盟广告','视频广告','直接访问','搜索引擎']
    },
    toolbox: {
        feature: {
            saveAsImage: {}
        }
    },
    grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
    },
    xAxis : [
        {
            type : 'category',
            boundaryGap : false,
            data : ['周一','周二','周三','周四','周五','周六','周日']
        }
    ],
    yAxis : [
        {
            type : 'value'
        }
    ],
    series : [
        {
            name:'邮件营销',
            type:'line',
            stack: '总量',
            areaStyle: {},
            data:[120, 132, 101, 134, 90, 230, 210]
        },
        {
            name:'联盟广告',
            type:'line',
            stack: '总量',
            areaStyle: {},
            data:[220, 182, 191, 234, 290, 330, 310]
        },
        {
            name:'视频广告',
            type:'line',
            stack: '总量',
            areaStyle: {},
            data:[150, 232, 201, 154, 190, 330, 410]
        },
        {
            name:'直接访问',
            type:'line',
            stack: '总量',
            areaStyle: {normal: {}},
            data:[320, 332, 301, 334, 390, 330, 320]
        },
        {
            name:'搜索引擎',
            type:'line',
            stack: '总量',
            label: {
                normal: {
                    show: true,
                    position: 'top'
                }
            },
            areaStyle: {normal: {}},
            data:[820, 932, 901, 934, 1290, 1330, 1320]
        }
    ]
        };
         myChart.setOption(option);
      //配置统计图参数
      }
  }
}
</script>
<style>
  .btn{
    width:auto;
    height:auto;
    border:0px;
    justify-content: space-between;
    background-color:transparent;

  }
  .btn>h4{
    margin-bottom:3px;
  }
  .btn:hover{
    background-color:#e1e2e3;
  }
  .title{
    
  }
  .indexLeft{
    /*display:flex flex-column;*/
    padding:1%;
    width:50%;
  }
  .h1_card{
    display:inline-block;
    margin-bottom:2%;
    width:25%;
  }
  .test{
    background-color: #000;
  }
</style>