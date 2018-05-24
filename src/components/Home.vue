<!-- 首页 -->
<template>
  <div class="Home">
    <!-- 搜索框 -->
    <div class="search">
      <mt-search v-model="value" placeholder="" cancel-text=""></mt-search>
    </div>
      
    <!-- 轮播图 -->
    <div class="swipe">
      <mt-swipe :auto="4000">
        <mt-swipe-item><router-link to="bedding"><img src="static/img/index/article-head.jpg" alt="轮播图"></router-link></mt-swipe-item>
        <mt-swipe-item><router-link to="all"><img src="static//img/index/article-more.jpg" alt="轮播图"></router-link></mt-swipe-item>
      </mt-swipe>
    </div>

    <!-- 迷你菜单 -->
    <div class="HomeList">
      <ul >
            <li>
              <div @click="chuangping">
                <img src="/static/img/index/bedding.png" alt="床上用品">
                <span>床上用品</span>
              </div>
            </li>
            <li>
              <div @click="sofas">
                <img src="/static/img/index/shafa.png" alt="沙发">
                <span>沙发</span>
              </div>
            </li>
            <li>
              <div @click="curtains">
                <img src="/static/img/index/chuanglian.png" alt="窗帘">
                <span>窗帘</span>
              </div>
            </li>
            <li>
              <div @click="cupboards">
                <img src="/static/img/index/chugui.png" alt="橱柜">
                <span>橱柜</span>
              </div>
            </li>
            <li>
              <div @click="wardrobes">
                <img src="/static/img/index/yigui.png" alt="衣柜">
                <span>衣柜</span>
              </div>
            </li>
            <li>
              <div @click="btn">
                <img src="/static/img/index/weiyu.png" alt="卫浴">
                <span>卫浴</span>
              </div>
            </li>
            <li>
              <div @click="btn">
                <img src="/static/img/index/diban.png" alt="地板">
                <span>地毯</span>
              </div>
            </li>
            <li>
              <div @click="btn">
                <img src="/static/img/index/huaping.png" alt="摆件">
                <span>摆件</span>
              </div>
            </li>
      </ul>
    </div>

    <!-- 精选好物 -->
      <div class="main">
        <span >精选好物</span>
        <div class="main_box">
            <ul>
              <li v-for="(todo,index) in todos" :id="todo.id"  @click="open(todo.id)" class="list">
                  <div class="image">
                      <img v-bind:src="todo.ImgF" alt="图片">
                  </div>
                  <div class="name">{{todo.name}}</div>
                  <div class="Price">￥{{todo.Price}}</div> 
              </li>
            </ul>
        </div>
      </div>
  </div>
</template>

<script>
//import { mapState,mapMutations,mapGetters  } from 'vuex';
import { Swipe, SwipeItem } from 'mint-ui';
import { MessageBox } from 'mint-ui';
import store from '../vuex/store.js';
export default {
  name:"Home",
  data(){
    return{
      todos:[],
      value: ''
    }
  },
  mounted:function(){
    this.getData();
  },
  methods:{
    getData:function(){
      var _this=this;
      this.$http.get("/static/Home.json").then(function(res) {
        for (var i = 0, len = res.body.todos.length; i < len; i++) {
          var selData = res.body.todos[i];
          var part = res.body.todos[i].name;
          _this.todos.push(selData);
        }
      })
    },
    open:function(id){
      this.$router.push({path:"goodDetail",query:{id:id}})  //跳转到goodDetail组件，路由中加入查询参数
    },
    chuangping:function(){
      this.$router.push({path:"bedding"})
    },
    sofas:function(){
      this.$router.push({path:"sofas"})
    },
    curtains:function(){
      this.$router.push({path:"curtains"})
    },
    cupboards:function(){
      this.$router.push({path:"cupboards"})
    },
    wardrobes:function(){
      this.$router.push({path:"wardrobes"})
    },
    bathrooms:function(){
      this.$router.push({path:"bathrooms"})
    },
    btn:function(){
      MessageBox('提示', 'Thank you');
    }
  },
}
</script>

<style>
  .Home .mint-searchbar{
      background-color: #f7f7f7;
      position:fixed;
      width:100%;
  }
  .Home .mint-search{
      height: 100%;
      overflow: hidden;
  }
  .Home .mint-searchbar-inner .mintui-search{
      font-size: 20px;
  }
  .Home .mint-searchbar-cancel{
      color: red;
      margin-left: 0px;
  }
 .Home .swipe{
   height: 6.5rem;
   /*margin-top: 1.3rem;*/
  }
  .Home .swipe img{
    width: 100%;
    height: 6.5rem;
  }
  .Home ul li{
    list-style: none;
  }
  .Home .HomeList{
    width: 100%;
    height: 4.2rem;
    background: white;
    border-bottom: 1px solid #cccccc;
  }
  .Home .HomeList>ul>li{
    width: 25%;
  }
  .Home .HomeList>ul>li div{
    /* width: 60px; */
    width: 1.7rem;
    /* height: 58px; */
    height: 1.68rem;
    margin: auto;
    text-align:center;
  }
  .Home .HomeList>ul>li img{
    display: block;
    width: 55%;
    height: 60%;
    margin: 12px auto 0 auto;
  }
  .Home .HomeList>ul>li span{
    display:block;
    font-size: 0.42rem;
    line-height: 0.7rem;

  }
  .Home .HomeList>ul>li{
    float: left;
    margin: auto;
  }
  .Home .main_box{
    height: 339px;
  }
  .Home .main span{
    display: block;
    height: 1.3rem;
    background: white;
    font-size: 0.6rem;
    line-height: 1.5rem;
    padding-left: 0.3rem;
    border-bottom: 1px solid #cccccc;
  }
  .Home .list {
    height: 6.3rem;
    background: white;
    float: left;
    box-sizing:border-box;
    width:50%;
    border-left: 2px solid #F4F4F4;
    border-bottom: 2px solid #F4F4F4;
  }
  .Home .list span{
    display: block;
    color: red;
    padding-left: 0.5rem;
    padding-top: 0.1rem;
  }
  .Home .main_box ul{
    overflow: hidden;
    margin-bottom: 1.5rem;
  }  
  .Home .image{
    width: 100%;
     height: 3.7rem;
    background: white;
  }
  .Home .image img{
    height: 3.5rem;
    width: 3.5rem;
    display: block;
    margin: auto;
    padding-top: 0.5rem;
  }  
  .Home .name{
    width: 80%;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    margin: auto;
    font-size: 0.45rem;
    padding-top: 0.6rem;
    font-weight: 500;
    text-align: center;
  } 
  .Home .Price{
    font-size: 0.33rem;
      color: red;
      margin: auto;
      /* padding: 0.1rem 0.9rem; */
      text-align: center;
      padding-top: 0.3rem;
      font-weight: bold; 
      font-size: 0.38rem;
  }
  .Home .official{
    width: 100%;
      height: 0.8rem;
      background: white;
      margin-top: 1.33rem;
  }
</style>

