<template>
  <div id="left-nav" class="left-nav">
    <ul class="wrapper">
        <li  v-for="list in navList" :class="['icon', 'iconfont', list.clazz]">
          <a>{{list.nameZH}}</a>
        </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'leftNav',
  data () {
    return {
        navList:[
            {clazz:'icon-wodezichan', nameZH:'收银'},
            {clazz:'icon-hanbao', nameZH:'商店'},
            {clazz:'icon-hanbao', nameZH:'会员'},
            {clazz:'icon-shijian', nameZH:'统计'},
        ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
    .left-nav{
       color:#fff;
       font-size:10px;
       height:100%;
       background-color: #1D8ce0;
       display: inline-block; 
       float:left;     
       width:5%;
       min-width: 90px;
    }
    .iconfont{
       font-size:30px;
    }
    .left-nav li{
        list-style: none;
        text-align: center;
        border-bottom:1px solid #20a0ff;
        padding:10px;
    }
    .left-nav li:hover{
      background-color: #20a0ff;
    }
    .left-nav li a{
      display:inline-block;
      font-size: 20px;
    }
    
    .icon-wodezichan:before,.icon-hanbao:before,.icon-huiyuanqia:before,.icon-shijian:before
    {
      width: 100%;
      height: 30px;
      display: inline-block;
    }
</style>
