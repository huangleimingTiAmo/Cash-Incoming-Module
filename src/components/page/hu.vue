<template>
  <el-col :span="7" class="pos-order" id="order-list">
          <el-tabs>
            <el-tab-pane label="点餐">
              <el-table :data="tableData" border show-summary style="width:100%">
                <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                <el-table-column prop="count" label="数量" width="70"></el-table-column>
                <el-table-column prop="price" label="金额" width="70"></el-table-column>
                <el-table-column  label="操作" width="100" fixed="right">
                  <template slot-scope="scope">
                    <el-button type="text" size="small">删除</el-button>
                    <el-button type="text" size="small">增加</el-button> 
                  </template>
                </el-table-column>                                          
              </el-table>
              <div class="divbtn">
                <el-button type="warning" >挂单</el-button>
                <el-button type="danger" >删除</el-button>
                <el-button type="success" >结账</el-button>
              </div>
            </el-tab-pane>
            <el-tab-pane label="挂单">

            </el-tab-pane>
            <el-tab-pane label="外卖">
              
            </el-tab-pane>                    
          </el-tabs>
        </el-col>
</template>
