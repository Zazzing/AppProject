<!-- 沙发 -->
<template>
    <div class="sofas">
        <!-- 头部 -->
        <div class="sofasHeader">
            <a href="#" @click="sofas">
                <i class="iconfont icon-552cc14536532"></i>
            </a>
            <span>沙发</span>
        </div>
        <div class="sofasMain">
            <mt-navbar v-model="selected">
                <mt-tab-item id="tab-container1">全部</mt-tab-item>
                <mt-tab-item id="tab-container2">布艺风</mt-tab-item>
                <mt-tab-item id="tab-container3">北欧风</mt-tab-item>
                <mt-tab-item id="tab-container4">简约风</mt-tab-item>
            </mt-navbar>
            <mt-tab-container v-model="selected" swipeable>
                <!-- 全部 -->
                <mt-tab-container-item id="tab-container1">
                    <ul style="margin-top: 2px;">
                        <li class="_sofasList" v-for="(sofas,index) in sofalists" @click="open(sofas.id)">
                            <img v-bind:src="sofas.ImgF" alt="图片">
                            <p>{{sofas.name}}</p>
                            <div>￥{{sofas.Price}}</div>
                        </li>
                    </ul>
                </mt-tab-container-item>
                <!-- 布艺沙发 -->
                <mt-tab-container-item id="tab-container2">
                    <ul style="margin-top: 2px;">
                        <li class="_sofasList" v-for="(sofas,index) in fabric" @click="open(sofas.id)">
                            <img v-bind:src="sofas.ImgF" alt="图片">
                            <p>{{sofas.name}}</p>
                            <div>￥{{sofas.Price}}</div>
                        </li>
                    </ul>
                </mt-tab-container-item>
                <!-- 北欧沙发 -->
                <mt-tab-container-item id="tab-container3">
                    <ul style="margin-top: 2px;">
                        <li class="_sofasList" v-for="(sofas,index) in nordic" @click="open(sofas.id)">
                            <img v-bind:src="sofas.ImgF" alt="图片">
                            <p>{{sofas.name}}</p>
                            <div>￥{{sofas.Price}}</div>
                        </li>
                    </ul>
                </mt-tab-container-item>
                <!-- 简约沙发 -->
                <mt-tab-container-item id="tab-container4">
                    <ul style="margin-top: 2px;">
                        <li class="_sofasList" v-for="(sofas,index) in simple" @click="open(sofas.id)">
                            <img v-bind:src="sofas.ImgF" alt="图片">
                            <p>{{sofas.name}}<p>
                            <div>￥{{sofas.Price}}</div>
                        </li>
                    </ul>
                </mt-tab-container-item>
            </mt-tab-container>
        </div>
    </div>
</template>

<script>
import { Navbar, TabItem } from 'mint-ui';
export default {
    data(){
        return{
            selected:"tab-container1",
            sofalists:[],
            fabric:[],
            nordic:[],
            simple:[]
        }
    },
    mounted:function(){
        this.getData(),
        this.FabricData(),
        this.NordicData(),
        this.SimpleData()
    },
    methods:{
        getData:function(){
            var _this=this;
            this.$http.get("/static/sofa.json").then(function(res){
                for(var i=0,len=res.body.SofaLists.length;i<len;i++){
                    var selData=res.body.SofaLists[i];
                    //var sofas=res.body.sofas[i].name;
                    _this.sofalists.push(selData)
                }
            })
        },
        FabricData:function(){
            var _this=this;
            this.$http.get("/static/sofa.json").then(function(res){
                for(var i=0,len=res.body.Fabric.length;i<len;i++){
                    var selData=res.body.Fabric[i];
                    //var fabric=res.body.Fabric[i].name;
                    _this.fabric.push(selData)
                }
            })
        },
        NordicData:function(){
            var _this=this;
            this.$http.get("/static/sofa.json").then(function(res){
                for(var i=0,len=res.body.Nordic.length;i<len;i++){
                    var selData=res.body.Nordic[i];
                    //var nordic=res.body.Nordic[i].name;
                    _this.nordic.push(selData)
                }
            })
        },
        SimpleData:function(){
            var _this=this;
            this.$http.get("/static/sofa.json").then(function(res){
                for(var i=0,len=res.body.Simple.length;i<len;i++){
                    var selData=res.body.Simple[i];
                    var simple=res.body.Simple[i].name;
                    _this.simple.push(selData)
                }
            })
        },
        sofas:function(){
            this.$router.push({path:"Home"})
        },
        open:function(id){
            this.$router.push({path:"goodDetail",query:{id:id}})
        },
    }
}
</script>


<style>
    .sofasHeader{
        position: fixed;
        width: 100%;
       /* -webkit-box-shadow: none;
        box-shadow: none;*/
        height: 1.3rem;
        line-height: 1.3rem;
        font-size: 0.52rem;
        padding-left: 0.3rem;
        background: white;
        top: 0;
        z-index: 100;
        border-bottom: 2px solid #F4F4F4;
    }
    .sofasHeader i{
        display: block;
        float: left;
        height: 50px;
        padding-right: 0.3rem;
        font-size: 22px;
        color: black;
    }
    .sofas .mint-navbar .mint-tab-item.is-selected {
        border-bottom: 3px solid red;
        color: red;
    }
    ._sofasList{
        height: 7rem;
        background: white;
        float: left;
        box-sizing: border-box;
        width: 50%;
        border-right: 1px solid #F4F4F4;
        border-bottom: 3px solid #F4F4F4;
        border-left: 1px solid #F4F4F4;
        float: left;
        margin-top: 1px;
        list-style: none;
    }
    .sofasMain{
        margin-top: 1.43rem;
    }
    ._sofasList p{
        width: 94%;
        overflow: hidden;
        text-overflow: ellipsis;
        margin: auto;
        font-size: 0.43rem;
        text-align: center;
        white-space: nowrap;
    }
    ._sofasList div{
        text-align: center;
        color: red;
        margin-top: 10px;
        font-size: 0.45rem;
    }
    ._sofasList img{
        height: 4rem;
        width: 4rem;
        display: block;
        margin: auto;
        padding: 0.5rem;
    }
    .sofas .mint-tab-item-label {
        color: inherit;
        font-size: 0.45rem;
        line-height: 0.5rem;
    }
</style>
