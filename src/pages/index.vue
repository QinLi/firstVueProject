<template>
  <div class="index-wrap w1200 clearfix">
    <div class="index-left">
      <div class="index-left-block">
        <h2>全部产品</h2>
        <!--
        <h3>pc产品</h3>
        <ul>
          <li><a href="#">数据统计</a></li>
          <li><a href="#">数据预测</a></li>
          <li><a href="#">流量分析</a></li>
          <li><a href="#">广告发布</a></li>
        </ul>
        <div class="hr"></div>
        <h3>手机应用类</h3>
        <ul>
          <li><a href="#">91助手</a></li>
          <li><a href="#">产品助手</a></li>
          <li><a href="#">智能地图</a></li>
          <li><a href="#">团队语音</a></li>
        </ul>
      -->
      <template v-for="product in productList">
        <h3>{{product.title}}</h3>
        <ul>
          <li v-for="item in product.list">
            <a :href="item.url">{{item.name}}</a>
            <span v-if="item.hot" class="hot">HOT</span>
          </li>
        </ul>
        <div v-if="!product.last" class="hr"></div>
      </template>

      </div>
      

      <div class="index-left-block">
        <h2>最新消息</h2>
        <ul>
          <li v-for="item in newsList">
            <a :href="item.url" class="new-item TXTovehid">{{item.title}}</a>
          </li>
        </ul>
      </div>


    </div>

    <div class="index-right">

      <slide-show :slides="slides" :inv="slideSpeed"></slide-show>

      <div class="index-border-list clearfix">
        <div class="index-board-item" v-for="(item, index) in borderList" :class="[{'line-last': index % 2 !== 0},'index-board-' + item.id]">
          <div class="index-board-item-inner">
            <h2>{{item.title}}</h2>
            <p>{{item.description}}</p>
            <div class="index-board-button">
              <!-- <a v-bind:href="item.url" class="button">立即购买</a> -->
              <router-link class="button" :to="{path: 'detail/'+item.toKey}">立即购买</router-link> 
            </div>
          </div>
        </div>
      </div>
      
    </div>
  </div>
</template>

<script>
import slideShow from '../components/slideShow'
export default {
  created: function () {
    this.$http.post('api/getNewsList').then(function (res) {
      this.newsList = res.data
    }, function (err) {
      console.log(err)
    })
  },
  components: {
    slideShow
  },
  data () {
    return {
      slideSpeed: 3000,
      slides: [
        {
          src: require('../assets/slideShow/pic1.jpg'),
          title: 'xxx1',
          href: 'detail/analysis'
        },
        {
          src: require('../assets/slideShow/pic2.jpg'),
          title: 'xxx2',
          href: 'detail/count'
        },
        {
          src: require('../assets/slideShow/pic3.jpg'),
          title: 'xxx3',
          href: 'detail/publish'
        },
        {
          src: require('../assets/slideShow/pic4.jpg'),
          title: 'xxx4',
          href: 'detail/forecast'
        }
      ],
      productList: {
        pc: {
          title: 'pc产品',
          list: [
            {
              name: '数据统计',
              hot: true,
              url: 'http://starcraft.com'
            },
            {
              name: '数据预测',
              url: 'http://warcraft.com'
            },
            {
              name: '流量分析',
              url: 'http://overwatch.com'
            },
            {
              name: '广告发布',
              url: 'http://hearstone.com'
            }
          ]
        },
        app: {
          title: '手机应用类',
          last: true,
          list: [
            {
              name: '91助手',
              url: 'http://weixin.com'
            },
            {
              name: '产品助手',
              url: 'http://twitter.com'
            },
            {
              name: '智能地图',
              url: 'http://maps.com'
            },
            {
              name: '团队语音',
              url: 'http://phone.com'
            }
          ]
        }
      },
      newsList: [],
      borderList: [
        {
          title: '开放产品',
          description: '开放产品是一款开放产品',
          id: 'car',
          toKey: 'analysis',
          saleOut: false
        },
        {
          title: '品牌营销',
          description: '品牌营销帮助你的产品更好地找到定位',
          id: 'earth',
          toKey: 'count',
          saleOut: false
        },
        {
          title: '使命必达',
          description: '使命必达快速迭代永远保持最前端的速度',
          id: 'loud',
          toKey: 'forecast',
          saleOut: true
        },
        {
          title: '勇攀高峰',
          description: '帮你勇闯高峰，到达事业的顶峰',
          id: 'hill',
          toKey: 'publish',
          saleOut: false
        }
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.index-wrap{margin-top: 50px;font-family: "Microsoft Yahei";}
.index-left{width: 280px;float: left;}
.index-left-block{background: #fff;box-shadow: 0 0 1px #ddd;margin-bottom: 15px;}
.index-left-block h2{ background: #4fc08d;color: #fff;padding: 10px 15px;margin-bottom: 20px;}
.index-left-block h3{padding: 0 15px 5px 15px;font-weight: bold;color: #222;}
.index-left-block ul{ padding: 10px 15px;}
.index-left-block ul li{padding: 5px;}
.index-left-block .hr{height: 1px;background: #f8f5f8;margin: 0 10px 20px 10px;}
.hot{font-size: 12px;font-family: "Arial";background: red;color: #fff;padding: 0 5px;border-radius: 3px;}
.index-right{width: 900px;float: right;}
.index-right .index-border-list{}
.index-board-item{ float: left;width: 400px;background: #fff;box-shadow: 0 0 1px #ddd;
padding: 20px;margin-right: 20px;margin-bottom: 20px;}
.index-board-item-inner {min-height: 125px;padding-left: 120px;}
.index-board-car .index-board-item-inner{
  background: url(../assets/images/1.png) no-repeat;
}
.index-board-loud .index-board-item-inner{
  background: url(../assets/images/2.png) no-repeat;
}
.index-board-earth .index-board-item-inner{
  background: url(../assets/images/3.png) no-repeat;
}
.index-board-hill .index-board-item-inner{
  background: url(../assets/images/4.png) no-repeat;
}
.index-board-item h2 {
  font-size: 18px;
  font-weight: bold;
  color: #000;
  margin-bottom: 15px;
}
.line-last {
  margin-right: 0;
}
.index-board-button {
  margin-top: 20px;
}
.index-board-button .button{display: block;width: 100px;height: 36px;line-height: 36px;text-align: center;background: #4fc08d;color: #fff;}
.new-item{display: block;width: 230px;}

</style>
