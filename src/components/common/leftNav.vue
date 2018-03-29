<template>
  <div class="left-nav">
    <ul>
      <li>
        <i class="icon iconfont icon-goumai"></i>
        <div>收银</div>
      </li>
      <li>
        <i class="icon iconfont icon-dianpu"></i>
        <div>店铺</div>
      </li>
      <li>
        <i class="icon iconfont icon-hanbao"></i>
        <div>商品</div>
      </li>
      <li>
        <i class="icon iconfont icon-huiyuan"></i>
        <div>会员</div>
      </li>
      <li>
        <i class="icon iconfont icon-tongji"></i>
        <div>统计</div>
      </li>
    </ul>
    
  </div>
</template>
 
<script>
export default {
  name: 'leftNav',
  
}
</script>
 
 
<style>
 .left-nav{
   width: 5%;
   height: 100%;
   float: left;
   color:#fff;
   background-color: #1D8ce0;
   font-size: 12px
 }
 .iconfont{
   font-size: 25px
 }
 .left-nav ul{
   padding: 0px;
   margin: 0px;
 }
 .left-nav li{
   list-style: none;
   text-align: center;
   padding: 15px;
   border-bottom: 1px solid #20a0ff;
 }
</style>