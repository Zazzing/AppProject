<!-- 卫浴页面 -->
<template>
  <div class="bathroom">
    <!-- 头部 -->
    <div class="bathroomheader" >
      <router-link to="/">
        <i class="iconfont icon-552cc14536532"></i>
      </router-link>
      卫浴
    </div>
    <div class="_bathroom_twoMain">
      <ul style="margin-top: 2px;">
        <li class="_bathroomList" v-for="(bathroom,index) in bathroom" :id="bathroom.id" @click="open(bathroom.id)">
          <img v-bind:src="bathroom.ImgF" alt="图片">
          <p>{{bathroom.name}}</p>
          <div>￥{{bathroom.Price}}</div>
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
        bathroom:[]
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
          for(var i=0,len=res.body.bathrooms.length;i<len;i++){
            var selData=res.body.bathrooms[i];
            var part=res.body.bathrooms[i].name;
            _this.bathroom.push(selData)
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
  .bathroomheader{
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
  .bathroomheader i{
    display: block;
    float: left;
    height: 50px;
    padding-right: 0.3rem;
    font-size: 22px;
    color: black;
  }
  ._bathroomList{
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
  ._bathroom_twoMain{
    margin-top: 1.43rem;
  }
  ._bathroomList p{
    width: 94%;
    overflow: hidden;
    text-overflow: ellipsis;
    margin: auto;
    font-size: 0.43rem;
    text-align: center;
    white-space: nowrap;
  }
  ._bathroomList div{
    text-align: center;
    color: red;
    margin-top: 10px;
    font-size: 0.45rem;
  }
  ._bathroomList img{
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
