<!-- 橱柜页面 -->
<template>
  <div class="cupboard">
    <!-- 头部 -->
    <div class="cupboardheader" >
      <router-link to="/">
        <i class="iconfont icon-552cc14536532"></i>
      </router-link>
      橱柜
    </div>
    <div class="_cupboard_twoMain">
      <ul style="margin-top: 2px;">
        <li class="_cupboardList" v-for="(cupboard,index) in cupboard" :id="cupboard.id" @click="open(cupboard.id)">
          <img v-bind:src="cupboard.ImgF" alt="图片">
          <p>{{cupboard.name}}</p>
          <div>￥{{cupboard.Price}}</div>
        </li>
      </ul>
      <div class="clearfloat"></div>
    </div>
  </div>
</template>


<script>
import { Navbar, TabItem } from 'mint-ui';
export default {
  name:"cupboard",
  data(){
      return{
          cupboard:[]
      }
  },
  mounted:function(){
    this.getData()
  },
  methods:{
    // 全部
    getData:function(){
        var _this=this;
        this.$http.get("/static/others.json").then(function(res){
          for(var i=0,len=res.body.cupboards.length;i<len;i++){
            var selData=res.body.cupboards[i];
            var part=res.body.cupboards[i].name;
            _this.cupboard.push(selData)
        }
      })
    },
    open:function(id){
      this.$router.push({path:"goodDetail",query:{id:id}})
    }
  }
}
</script>

<style>
  .cupboardheader{
    position: fixed;
    width: 100%;
    height: 1.3rem;
    line-height: 1.3rem;
    font-size: 0.52rem;
    padding-left: 0.3rem;
    background: white;
    top: 0;
    z-index: 100;
    border-bottom: 2px solid #F4F4F4;
  }
  .cupboardheader i{
    display: block;
    float: left;
    height: 50px;
    padding-right: 0.3rem;
    font-size: 22px;
    color: black;
  }
  ._cupboardList{
    height: 7rem;
    background: white;
    float: left;
    box-sizing: border-box;
    width: 50%;
    border-right: 1px solid #F4F4F4;
    border-bottom: 1px solid #F4F4F4;
    /*border-left: 1px solid #F4F4F4;*/
    float: left;
    margin-top: 1px;
    list-style: none;
  }
  ._cupboard_twoMain{
    margin-top: 1.43rem;
  }
  ._cupboardList p{
    width: 94%;
    overflow: hidden;
    text-overflow: ellipsis;
    margin: auto;
    font-size: 0.43rem;
    text-align: center;
    white-space: nowrap;
  }
  ._cupboardList div{
    text-align: center;
    color: red;
    margin-top: 10px;
    font-size: 0.45rem;
  }
  ._cupboardList img{
    height: 4rem;
    width: 4rem;
    display: block;
    margin: auto;
    padding: 0.5rem;
  }
  .clearfloat{
    clear:both;
    height:0;
    font-size: 1px;
    line-height: 0px;
  } 
</style>
