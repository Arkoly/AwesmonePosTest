<template>
  <div class="pos" id="pos">
    <el-row>
      <el-col :span='7' class="pos-order" id="order-list">
        <el-tabs>
          <el-tab-pane  label="点餐">
            <el-table :data="tableData" border style="width:100%">
              <el-table-column prop="goodsName" label="商品名称"></el-table-column>
              <el-table-column prop="count" label="数量" width="50"></el-table-column>
              <el-table-column prop="price" label="金额" width="70"></el-table-column>
              <el-table-column label="操作" width="100" fixed="right">
                <template slot-scope="scope">
                  <el-button type="text" size="small"  @click="delSingleGood(scope.row,tableData)">删除</el-button>
                  <el-button type="text" size="small" @click="addOrderList(scope.row,tableData)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="total-goods">
                <span><small>数量：</small>{{totalCount}}</span>
                <span><small>金额：</small>{{totalMoney}}元</span>
            </div>
            <div class="div-btn">
              <el-button type="warning" @click="pendingOrder(pendingBox.pendingData)">挂单</el-button>
              <el-button type="danger" @click="delAllGoods()">删除</el-button>
              <el-button type="success" @click="checkout()">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">
            <el-table :data="pendingBox.pendingData" border style="width:100%">
              <el-table-column prop="goodsName" label="商品名称"></el-table-column>
              <el-table-column prop="count" label="数量" width="50"></el-table-column>
              <el-table-column prop="price" label="金额" width="70"></el-table-column>
            </el-table>
            <div class="total-goods">
                <span><small>数量：</small>{{pendingBox.pendingCount}}</span>
                <span><small>金额：</small>{{pendingBox.pendingMoney}}元</span>
            </div>
            <div class="div-btn">
              <el-button type="danger" @click="delAllGoods()">删除</el-button>
              <el-button type="success" @click="checkout()">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="外卖">
            外卖
          </el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span='15'>
          <div class="often-goods">
            <div class="title">常用商品</div>
            <div class="often-goods-list">
              <ul>
                <li v-for="goods in oftenGoods" @click="addOrderList(goods,tableData)">
                  <span>{{goods.goodsName}}</span>
                  <span class="o-price">￥{{goods.price}}元</span>
                </li>
              </ul>
            </div>
          </div>
          <div class="goods-type">
            <el-tabs>
              <el-tab-pane label="汉堡">
                <ul class='cookList'>
                    <li v-for="goods in type0Goods" @click="addOrderList(goods,tableData)">
                        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                        <span class="foodName">{{goods.goodsName}}</span>
                        <span class="foodPrice">￥{{goods.price}}元</span>
                    </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="小吃">
                <ul class='cookList'>
                    <li v-for="goods in type1Goods" @click="addOrderList(goods,tableData)">
                        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                        <span class="foodName">{{goods.goodsName}}</span>
                        <span class="foodPrice">￥{{goods.price}}元</span>
                    </li>
                </ul>
              </el-tab-pane><el-tab-pane label="饮料">
                <ul class='cookList'>
                    <li v-for="goods in type2Goods" @click="addOrderList(goods,tableData)">
                        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                        <span class="foodName">{{goods.goodsName}}</span>
                        <span class="foodPrice">￥{{goods.price}}元</span>
                    </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="套餐">
               <ul class='cookList'>
                    <li v-for="goods in type3Goods" @click="addOrderList(goods,tableData)">
                        <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                        <span class="foodName">{{goods.goodsName}}</span>
                        <span class="foodPrice">￥{{goods.price}}元</span>
                    </li>
                </ul>
              </el-tab-pane>
            </el-tabs>
          </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'pos',
  data () {
    return {
      msg: 'Welcome to Your pos page',
      tableData: [],
      oftenGoods:[],
      type0Goods:[],
      type1Goods:[],
      type2Goods:[],
      type3Goods:[],
      totalCount: 0,
      totalMoney: 0,
      pendingBox:{
        pendingData:[],
        pendingCount: 0,
        pendingMoney: 0,
      },
    }
  },
  // computed:{
  //     orderHight:function(){
  //       return document.body.clientHeight;
  //     }
  // },
  created:function(){
    
    var showLocalOften = true;
    var showLocalType = true;
    // axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods')
    // .then(response=>{
    //   console.log(response)
    //   this.oftenGoods = response.data;
    //   showLocalOften = false;
    // })
    // .catch(error=>{
    //   console.log(error);
    //   console.log('网络错误，不能访问,显示本地数据');
    //   showLocalOften = true;
    // })

    // axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods')
    // .then(response=>{
    //   console.log(response)
    //   this.type0Goods = response.data[0];
    //   this.type1Goods = response.data[1];
    //   this.type2Goods = response.data[2];
    //   this.type3Goods = response.data[3];
    //   showLocalType = false;

    // })
    // .catch(error=>{
    //   console.log(error);
    //   console.log('网络错误，不能访问,显示本地数据');
    //   showLocalType = true;
    // })

    import('../../mockData.js').then(mod => {
      this.$nextTick(() => {
        // this.tableData = mod.tableData;
        if(showLocalOften){
          this.oftenGoods = mod.oftenGoods;
        }
        if(showLocalType){
          
          this.type0Goods = mod.typeGoods[0];
          this.type1Goods = mod.typeGoods[1];
          this.type2Goods = mod.typeGoods[2];
          this.type3Goods = mod.typeGoods[3];
          // console.log(mod.typeGoods)
        }
      })
    });
    

  },
  computed:{
  },
  mounted:function(){
    this.resizeHeight();
    this.pendingBox.pendingData = this.getPendingData()
    
        
  },
  updated:function(){
  },
  methods:{
    getPendingData(){
      let obj = localStorage.getItem('localOrder');
      return JSON.parse(obj);
    },
    //点击挂单后，将tableData的点餐数据保存到浏览器中
    pendingOrder(data){
      if(this.tableData){
          //将数组对象转化为字符串
          let str = JSON.stringify(this.tableData)
          localStorage.setItem('localOrder', str);
          this.pendingBox.pendingData = this.tableData;
          this.tableData = [];
      }
      this.getAllMoney(data);
    },
    addOrderList(goods,data){
      let isHave = false;
      //判断左侧点餐列表中是否存在这个商品
      for(let i=0;i<this.tableData.length;i++){
        if(this.tableData[i].goodsId == goods.goodsId){
          isHave = true
        }
      }
      //根据isHave的值判断订单列表中是否已经有此商品
      if(isHave){
        //存在就进行数量增加
        let arr = this.tableData.filter(o => o.goodsId == goods.goodsId)
        //arr是一个新数组，arr[{goodsId:*,goodsName:*,price:*,count:*}],所以访问count需要用arr[0].count访问
        arr[0].count++;
      }else{
      //不存在就推入数组
        let newGoods = {goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1}
        this.tableData.push(newGoods)
      }
      this.getAllMoney(data);
    },
    delSingleGood(goods,data){
      // this.tableData = this.tableData.filter(o => o.goodsId != goods.goodsId);
      let arr = this.tableData.filter(o => o.goodsId == goods.goodsId)
      if(arr[0].count<=1){
        this.tableData = this.tableData.filter(o => o.goodsId != goods.goodsId);
      }else{
        arr[0].count--;
      }
      this.getAllMoney(data);
    },
    delAllGoods(){
      if(this.tableData){
        this.totalCount = 0;
        this.totalMoney = 0;
        this.tableData=[];
      }
      if(this.pendingBox.pendingData){
        this.pendingBox.pendingData = [];
        this.pendingBox.pendingCount= 0;
        this.pendingBox.pendingMoney= 0;
      }
    },
    //汇总全部金额和数量
    getAllMoney(data){
      this.totalCount = 0;
      this.totalMoney = 0;
      this.pendingBox.pendingCount= 0;
      this.pendingBox.pendingMoney= 0;
      //进行数量和价格的汇总计算
      if(data===this.tableData){
        data.forEach((element) => {
          this.totalCount = this.totalCount+element.count;
          this.totalMoney = this.totalMoney + (element.price*element.count);
        });
      }else{
        console.log('pendingData')
        console.log(this.pendingBox.pendingData)
        data.forEach((element) => {
          this.pendingBox.pendingCount = this.pendingBox.pendingCount+element.count;
          this.pendingBox.pendingMoney = this.pendingBox.pendingMoney + (element.price*element.count);
        });
      }
    },
    checkout(){
      if(this.totalCount!=0){
        this.totalCount = 0;
        this.totalMoney = 0;
        this.tableData=[];
        this.$message({
          message: '结账完成！',
          type: 'success'
        });
      }else{
        this.$message.error('遇到错误，无法完成结账！');
      }
    },
    resizeHeight(){
      var orderHight = document.body.clientHeight;
      window.onresize=function(){
          orderHight = document.body.clientHeight;
          console.log(orderHight)
          document.getElementById('pos').style.height = orderHight +'px'
      }
       
      document.getElementById('pos').style.height = orderHight +'px'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul li {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.pos{
  min-width: 1400px;
}
.pos-order{
}
.div-btn{
  margin-top: 10px;
}
.title{
      height: 20px;
      border-bottom:1px solid #D3DCE6;
      background-color: #F9FAFC;
      padding:10px;
  }
  .often-goods-list ul li{
    list-style: none;
    float:left;
    border:1px solid #E5E9F2;
    padding:10px;
    margin:5px;
    background-color:#fff;
    cursor: pointer;
  }
.o-price{
    color:#58B7FF; 
  }

  .goods-type{
    clear: both;
  }
.cookList li{
      list-style: none;
      width:23%;
      border:1px solid #E5E9F2;
      height: auto;
      overflow: hidden;
      background-color:#fff;
      padding: 2px;
      float:left;
      margin: 2px;
      cursor: pointer;
}
.cookList li span{
    
  display: block;
  float:left;
}
.total-goods{
  background-color:#fff;
  border-bottom:1px solid #E5E9F2;
  padding: 10px;
}
.foodImg{
    width: 40%;
}
.foodName{
    width: 118px;
    font-size: 18px;
    padding-left: 10px;
    color:brown;

}
.foodPrice{
    font-size: 16px;
    padding-left: 40px;
    padding-top:10px;
}
</style>
