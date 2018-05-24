<!-- 橱柜页面 -->
<template>
  <div class="all">
    <!-- 头部 -->
    <div class="allheader" >
      <router-link to="/">
        <i class="iconfont icon-552cc14536532"></i>
      </router-link>
      全部
    </div>
    <div class="allNav">
        <ul>
            <li>
                <p v-bind:class="{ price: isPrice }">价格</p>
                <span class="desOrder" @click="Ascorder()" v-bind:class="{ Asc: isAsc }">
                    {{this.Asc}}
                </span>
                <span class="desOrder" @click="Desorder()" v-bind:class="{ Des: isDes }">
                    {{this.Des}}
                </span>
            </li>
            <li v-bind:class="{ active: isActive }" @click="Goodsales()">
                <p>销量优先</p>
            </li>
        </ul>
    </div>

    <div class="_all_twoMain">
      <ul style="margin-top: 2px;">
        <li class="_allList" v-for="(allone,index) in allone" :id="allone.id" @click="open(allone.id)">
          <img v-bind:src="allone.ImgF" alt="图片">
          <p>{{allone.name}}</p>
          <div>￥{{allone.Price}}</div>
        </li>
      </ul>
      <div class="clearfloat"></div>
    </div>
  </div>
</template>


<script>
import { Navbar, TabItem } from 'mint-ui';
export default {
  name:"all",
  data(){
      return{
          all:[],
          allone:[],
          Des:"↓",
          Asc:"↑",
          isAsc:false,
          isDes:false,
          isActive:true,
          isPrice:false
      }
  },
  mounted:function(){
    this.getData()
  },
  methods:{
    // 全部
    getData:function(){
        var _this=this;
        this.$http.get("/static/data.json").then(function(res){
            for(var i=0,len=res.body.All.length;i<len;i++){
                var selData=res.body.All[i];
                var part=res.body.All[i].name;
                _this.all.push(selData);
            }
        })
        this.allone=this.all;
        this.num=this.Asc;
    },
    //升序
    Ascorder:function(){
        this.isActive=false;
        this.isPrice=true;
        this.isAsc=true;
        this.isDes=false;
        var _this=this;
        var allAsc=JSON.parse(JSON.stringify(this.allone));
        for(var i=0;i<allAsc.length-1;i++){
            for(var j=i+1;j<allAsc.length;j++){
                if((allAsc[i]['Price'] - allAsc[j]['Price'])>0){
                    var temp = allAsc[i];
                    allAsc[i] = allAsc[j];
                    allAsc[j] = temp;
                }
            }
        this.allone=allAsc;
        };
    },
    // 降序
    Desorder:function(){
        this.isActive=false;
        this.isAsc=false;
        this.isDes=true;
        this.isPrice=true;
        var _this=this;
        var allDes=JSON.parse(JSON.stringify(this.allone));
            for(var i=0;i<allDes.length-1;i++){
                for(var j=i+1;j<allDes.length;j++){
                    if((allDes[i]['Price'] - allDes[j]['Price'])<0){
                        var temp = allDes[j];
                        allDes[j] = allDes[i];
                        allDes[i] = temp;
                    }
                }
            };
            this.allone=allDes;
    },
    //点击销量优先
    Goodsales:function(){
        this.isActive=true;
        this.isAsc=false;
        this.isDes=false;
        this.isPrice=false;
        console.log(this.allone);
        console.log(this.all);
        this.allone=JSON.parse(JSON.stringify(this.all));
    },
    open:function(id){
      this.$router.push({path:"goodDetail",query:{id:id}})
    }
  }
}
</script>

<style>
  .allheader{
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
  .allheader i{
    display: block;
    float: left;
    height: 50px;
    padding-right: 0.3rem;
    font-size: 22px;
    color: black;
  }
  ._allList{
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
  .allNav{
    margin-top: 1.43rem;
  }
  .allNav ul{
    height: 1rem;
    line-height: 1rem;
    display: box;
    display: -webkit-box;
    display: -moz-box;
    background: #f8f8f8;
  }
  .allNav ul li{
    width:50%;
    box-flex: 1;
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    text-align: center;
    position: relative;
    font-size: 0.45rem;
    background: white;
    border-right: 2px solid #F4F4F4;
    /*font-weight: 550;*/
  }
  .allNav ul li{
    width:50%;
    box-flex: 1;
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    text-align: center;
    position: relative;
    font-size: 0.45rem;
    background: white;
    border-right: 2px solid #F4F4F4;
    /*font-weight: 550;*/
  }
  .allNav ul li p{
    display: inline-block;
  }
  .allNav ul .price{
    font-weight: 550;
    color: red;
  }
  .allNav ul .active{
    color: red;
    font-weight: 550;
  }
  .allNav ul .Asc{
    color: red;
    font-weight: 550;
  }
  .allNav ul .Des{
    color: red;
    font-weight: 550;
  }
  .allNav ul li a {
    display: block;
    color: black;
  }
  .allNav ul li img {
    width: 6%;
    height: 6%;
  }
  /*._all_twoMain{
    margin-top: 1.43rem;
  }*/
  ._allList p{
    width: 94%;
    overflow: hidden;
    text-overflow: ellipsis;
    margin: auto;
    font-size: 0.43rem;
    text-align: center;
    white-space: nowrap;
  }
  ._allList div{
    text-align: center;
    color: red;
    margin-top: 10px;
    font-size: 0.45rem;
  }
  ._allList img{
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
