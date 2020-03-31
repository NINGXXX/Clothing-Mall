<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <RecommendView :recommends="recommends"/>
    <feature-view/>
    <tab-control class="tab-control" :titles="['流行','新款','精选']"></tab-control>
    <ul>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
      <li>你好</li>
    </ul>
  </div>
</template>

<script>
  import HomeSwiper from "./childComps/HomeSwiper";
  import RecommendView from "./childComps/RecommendView";
  import FeatureView from "./childComps/FeatureView";

  import NavBar from "components/common/navbar/NavBar";
  import tabControl from "components/content/tabControl/tabControl";

  import {getHomeMultidata,getHomeGoods} from "network/home";

  export default {
    name: "Home",
    components:{
      NavBar,
      HomeSwiper,
      RecommendView,
      FeatureView,
      tabControl
    },
    data(){
      return{
        banners:[],
        recommends:[],
        goods:{
          'pop':{page:0,list:[]},
          'new':{page:0,list:[]},
          'sell':{page:0,list:[]},
        }
      }
    },
    created() {
      //请求多个数据
      this.getHomeMultidata()

      //请求商品数据
      this.getHomeGoods('pop')
      //this.getHomeGoods('new')
      //this.getHomeGoods('sell')
    },
    methods:{
      getHomeMultidata(){
        getHomeMultidata().then(res=>{
          //console.log(res);
          this.banners=res.data.banner.list;
          this.recommends=res.data.recommend.list;
        })
      },

      getHomeGoods(type){
        //动态拿到page
        const page=this.goods[type].page + 1;
        getHomeGoods(type,page).then(res=>{
          this.goods[type].list.push(...res.data.list);
          this.goods[type].page += 1;
        })
      }
    },
  }
</script>

<style scoped>
  #home{
    padding-top: 44px;
  }
  .home-nav{
    background-color: var(--color-tint);
    color: #fff;

    position: fixed;
    left: 0;
    right: 0;
    top:0;
    z-index: 9;
  }

  .tab-control{
    position: sticky;
    top: 44px;
  }
</style>
