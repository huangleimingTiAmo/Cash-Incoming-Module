<template>
  <div class="pos">
    
      <el-row>
        <el-col :span="7" class="pos-order" id="order-list">
          <el-tabs>
            <el-tab-pane label="点餐">
              <el-table :data="tableData" border  style="width:100%">
                <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                <el-table-column prop="count" label="数量" width="70"></el-table-column>
                <el-table-column prop="price" label="金额" width="70"></el-table-column>
                <el-table-column  label="操作" width="100" fixed="right">
                  <template slot-scope="scope">
                    <el-button type="text" size="small" @click="delGoods(scope.row)">删除</el-button>
                    <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button> 
                  </template>
                </el-table-column>                                          
              </el-table>
              <div class="totalDiv">
                <span>数量：{{totalCount}}</span>
                <span>金额：{{totalManey}}</span>
              </div>
              <div class="divbtn">
                <el-button type="warning" >挂单</el-button>
                <el-button type="danger" @click="delAllGoods">删除</el-button>
                <el-button type="success" @click="checkout">结账</el-button>
              </div>
            </el-tab-pane>
            <el-tab-pane label="挂单">

            </el-tab-pane>
            <el-tab-pane label="外卖">
              
            </el-tab-pane>                    
          </el-tabs>
        </el-col>
        <el-col :span="17">
          <div class="often-goods"> 
            <div class="title">常用商品</div>
            <div class="often-goods-list">
              <ul>
                <li v-for="goods in oftenGoods" @click="addOrderList(goods)">
                  <span>{{goods.goodsName}}</span>
                  <span class="often-price">￥{{goods.price}}元</span>
                </li>
              </ul>
            </div>
          </div>

          <div class="goods-type">
            <el-tabs>
              <el-tab-pane label="汉堡">
                <div>
                  <ul class='cookList'>
                      <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                          <span class="foodImg"><img :src="goods.goodsImg" ></span>
                          <span class="foodName">{{goods.goodsName}}</span>
                          <span class="foodPrice">￥{{goods.price}}元</span>
                      </li>
                  </ul>
                </div>
                  
              </el-tab-pane>
              <el-tab-pane label="小食">
                <div>
                  <ul class='cookList'>
                      <li v-for="goods in type1Goods" @click="addOrderList(goods)">
                          <span class="foodImg"><img :src="goods.goodsImg" ></span>
                          <span class="foodName">{{goods.goodsName}}</span>
                          <span class="foodPrice">￥{{goods.price}}元</span>
                      </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="饮料">
                <div>
                  <ul class='cookList'>
                      <li v-for="goods in type2Goods" @click="addOrderList(goods)">
                          <span class="foodImg"><img :src="goods.goodsImg" ></span>
                          <span class="foodName">{{goods.goodsName}}</span>
                          <span class="foodPrice">￥{{goods.price}}元</span>
                      </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="套餐">
                  <div>
                  <ul class='cookList'>
                      <li v-for="goods in type3Goods" @click="addOrderList(goods)">
                          <span class="foodImg"><img :src="goods.goodsImg" ></span>
                          <span class="foodName">{{goods.goodsName}}</span>
                          <span class="foodPrice">￥{{goods.price}}元</span>
                      </li>
                  </ul>
                </div>
              </el-tab-pane>
      
            </el-tabs>
          </div>
        </el-col>
      </el-row>
    
  </div>
</template>
 
<script>
import axios from "axios";
export default {
  name: "pos",

  data() {
    return {
      tableData: [],
      oftenGoods: [],
      type0Goods: [],
      type1Goods: [],
      type2Goods: [],
      type3Goods: [],
      totalManey: 0,
      totalCount: 0
    };
  },
  methods: {
    addOrderList(goods) {
      //首先判断商品列表里是否含有选中商品
      // console.log(goods)
      let isHave = false;
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsId == goods.goodsId) {
          isHave = true;
        }
      }
      //根据isHave值进行判断
      if (isHave) {
        //存在就只进行数量增加
        let arr = this.tableData.filter(o => o.goodsId == goods.goodsId);
        //   function(o){
        //     return o.goodsId==goods.goodsId
        // }
        arr[0].count++;
      } else {
        //不存在就在列表里增加
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1
        };
        this.tableData.push(newGoods);
      }
      this.getAllCount();
    },
    // 删除单个商品
    delGoods(goods) {
      // console.log(goods)
      // console.log(this.tableData)
      this.tableData = this.tableData.filter(function(o) {
        return o.goodsId != goods.goodsId;
      });
      // console.log(this.tableData)
      this.getAllCount();
    },
    //刪除全部商品
    delAllGoods() {
      this.tableData = [];
      (this.totalManey = 0), (this.totalCount = 0);
    },
    // 计算总数

    getAllCount() {
      this.totalManey = 0;
      this.totalCount = 0;
      if (this.tableData) {
        for (let i = 0; i < this.tableData.length; i++) {
          this.totalCount += this.tableData[i].count;
          this.totalManey += this.tableData[i].count * this.tableData[i].price;
        }
      }
    },
    checkout() {
      if (this.totalCount != 0) {
        this.tableData = [];
        this.totalCount = 0;
        this.totalMoney = 0;
        this.$message({
          message: "结账成功",
          type: "success"
        });
      } else {
        this.$message.error("定單為空");
      }
    }
  },

  created() {
    axios
      .get("http://jspang.com/DemoApi/oftenGoods.php")
      .then(reponse => {
        // console.log(reponse)
        this.oftenGoods = reponse.data;
      })
      .catch(error => {
        // console.log(error)
        alert("网络连接失败");
      }),
      axios
        .get("http://jspang.com/DemoApi/typeGoods.php")
        .then(reponse => {
          // console.log(reponse)
          this.type0Goods = reponse.data[0];
          this.type1Goods = reponse.data[1];
          this.type2Goods = reponse.data[2];
          this.type3Goods = reponse.data[3];
        })
        .catch(error => {
          // console.log(error)
          alert("网络连接失败");
        });
  },
  mounted: function() {
    var orderHeight = document.body.clientHeight;
    // console.log(orderHeight)
    document.getElementById("order-list").style.height = orderHeight + "px";
  }
};
</script>
 
 
<style scoped>
.pos-order {
  background-color: #f9fafc;
  border-right: 1px solid #c0ccda;
}
.divbtn {
  margin-top: 10px;
  margin-left: 10px;
}
.title {
  height: 20px;
  border-bottom: 1px solid #d3dce5;
  background-color: #f9fafc;
  text-align: left;
  padding: 10px;
}
.often-goods-list ul li {
  list-style: none;
  float: left;
  border: 1px solid #e5e9f2;
  padding: 8px;
  margin: 5px;
  background-color: #fff;
  border-radius: 10px;
  cursor: pointer;
}
.often-goods-list ul li .often-price {
  color: rgb(136, 202, 252);
}
.goods-type {
  clear: both;
}
.cookList li {
  list-style: none;
  width: 23%;
  border: 1px solid #e5e9f2;
  border-radius: 8px;
  height: 90px;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 2px;
  cursor: pointer;
}
.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 50%;
}
.foodImg img {
  width: 100%;
  height: 100%;
}
.foodName {
  font-size: 16px;
  padding-left: 10px;
  color: rgb(197, 226, 32);
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
.totalDiv {
  background-color: rgba(221, 238, 237, 0.966);
  height: 35px;
  line-height: 35px;
}
</style>