<template>
	<view>
		<mysearch></mysearch>
    <view class="hmly-swiper-container">
      <swiper class="hmly-swiper" autoplay="true" circular="true"
        interval="3000" easing-function="easeOutCubic" :current="swiperCurrent" @change="swiperChange">
        <!-- 轮播图图片 -->
        <swiper-item class="hmly-swiper-item" v-for="(item, index) in imgList" :key="index">
          <!-- 加上widthFix可以使图片自适应 -->
          <image :src="item" mode="aspectFill"></image>
        </swiper-item>
      </swiper>
      <!-- 为了和喜马拉雅一致，自己需定制轮播图dots -->
      <view class="hmly-dots">
        <view v-for="dot in imgList.length" :key="dot">
          <view :class="['hmly-dots-item', dot == swiperCurrent ? ' hmly-dot-active' : '']"></view>
        </view>
      </view>
	  </view>
    
    <!-- 宫格导航 -->
    <view class="hmly-nav">
      <navigator class="hmly-nav-item" v-for="(item, index) in navList" :key="index" :url="`/pages/index/bangdan/index?ev=${item.events}`">
        <!-- 
          
          因为没有合适的图，所以全部使用的一样的 
          并且因为界面都是一致的就是内容不同，这里为了简单，使用的都是统一界面
  
          解决办法：你可以通过页面传参的方式来进行区分
          -->
        <image class="hmly-nav-icon" :src="item.icon" mode="widthFix" lazy-load="false"></image>
        <text class="hmly-nav-text">{{item.text}}</text>
      </navigator>
    </view>
    
    <!-- 猜你喜欢 -->
    <view class="hmly-like">
      <view class="hmly-bar-title">
        <view class="hmly-title-left">猜你喜欢</view>
        <view class="hmly-title-right">查看全部 <text class="icon-right"></text> </view>
      </view>
      <!-- 这没有没有使用数据绑定，因为是练手而且数据比较少 -->
      <view class="hmly-like-item-box">
        <view class="hmly-like-item" @tap="gotoDetails" :data-coverImg="item.coverMiddle" :data-title="item.intro" v-for="(item, index) in guess" :key="index">
          <view class="hmly-like-img">
            <image class="hmly-like-item-icon" :src="item.coverMiddle" mode="widthFix"></image>
            <view class="hmly-like-cover">
              <!-- text用来显示icon  暂无 -->
              <text class=""></text> {{ item.playsCounts | pc }}
            </view>
          </view>
          <view class="hmly-like-text">{{item.intro}}</view>
        </view>
      </view>
    </view>
    
    <!-- 有数据的时候显示 -->
    <block v-if="showitem">
      <!-- 有声小说 -->
      <view class="hmly-content-list">
        <view class="hmly-bar-title">
          <view class="hmly-title-left">有声小说</view>
          <view class="hmly-title-right">查看全部<text class="icon-right"></text></view>
        </view>
        <block v-for="(item, index) in xiaoshuocontent" :key="index">
          <view class="hmly-content" @tap="gotoDetails" :data-coverImg="item.albumCoverUrl290" :data-title="item.title">
            <view class="hmly-content-img">
              <image :src="item.albumCoverUrl290" mode="widthFix"></image>
            </view>
            <view class="hmly-content-right">
              <view class="hmly-content-title">
                <view class="hmly-title-text">{{item.title}}</view>
                <view class="hmly-introduction">{{item.trackTitle}}</view>
              </view>
              <view class="hmly-count">
                <view class="hmly-play-count">
                  <!-- <text class="icon-"></text> -->
                  126亿
                </view>
                <view class="hmly-ji-count">{{item.tracks}}集</view>
              </view>
            </view>
          </view>
        </block>
      </view>
      <!-- 相声评书 -->
      <view class="hmly-content-list">
        <view class="hmly-bar-title">
          <view class="hmly-title-left">相声评书</view>
          <view class="hmly-title-right">查看全部<text class="icon-right"></text></view>
        </view>
        <block v-for="(item, index) in xiangshengcontent" :key="index">
          <view class="hmly-content" @tap="gotoDetails" :data-coverImg="item.albumCoverUrl290" data-title="item.title">
            <view class="hmly-content-img">
              <image :src="item.albumCoverUrl290" mode="widthFix"></image>
            </view>
            <view class="hmly-content-right">
              <view class="hmly-content-title">
                <view class="hmly-title-text">{{item.title}}</view>
                <view class="hmly-introduction">{{item.trackTitle}}</view>
              </view>
              <view class="hmly-count">
                <view class="hmly-play-count">
                  <!-- <text class="icon-"></text> -->
                  126亿
                </view>
                <view class="hmly-ji-count">{{item.tracks}}集</view>
              </view>
            </view>
          </view>
        </block>
      </view>
      <!-- 脱口秀 -->
      <view class="hmly-content-list">
        <view class="hmly-bar-title">
          <view class="hmly-title-left">脱口秀</view>
          <view class="hmly-title-right">查看全部<text class="icon-right"></text></view>
        </view>
        <block v-for="(item, index) in tuokocontent" :key="index">
          <view class="hmly-content" @tap="gotoDetails" :data-coverImg="item.albumCoverUrl290" :data-title="item.title">
            <view class="hmly-content-img">
              <image :src="item.albumCoverUrl290" mode="widthFix" lazy-load="false"></image>
            </view>
            <view class="hmly-content-right">
              <view class="hmly-content-title">
                <view class="hmly-title-text">{{item.title}}</view>
                <view class="hmly-introduction">{{item.trackTitle}}</view>
              </view>
              <view class="hmly-count">
                <view class="hmly-play-count">
                  <!-- <view class="icon-"></view> -->
                  126亿
                </view>
                <view class="hmly-ji-count">{{item.tracks}}集</view>
              </view>
            </view>
          </view>
        </block>
      </view>
    </block>
    <block v-else>
      <view class="hmly-data-notip">
        <view class="hmly-tip">
          网络暂时走丢了，请稍后再试
        </view>  
      </view>
    </block>
	</view>
</template>

<script>
  import mysearch from '@/component/search'
	export default {
    components: {
      mysearch
    },
		data() {
			return {
				imgList: [
				  '../../static/ad1.jpg',
				  '../../static/ad2.jpg',
				  '../../static/ad3.jpg',
				  '../../static/ad4.jpg',
				  '../../static/ad5.jpg',
				  '../../static/ad6.jpg',
				  '../../static/ad7.jpg'
				],
				navList: [{
				    icon: '../../static/nav-icon/diantai.png',
				    events: 'goToBangDan',
				    text: '榜单'
				  },
				  {
				    icon: '../../static/nav-icon/diantai.png',
				    events: 'goToBangDan',
				    text: '听小说'
				  },
				  {
				    icon: '../../static/nav-icon/diantai.png',
				    events: 'goToBangDan',
				    text: '情感电台'
				  },
				  {
				    icon: '../../static/nav-icon/diantai.png',
				    events: 'goToBangDan',
				    text: '听知识'
				  }
				],
				swiperCurrent: 0,
        showitem: true,
        guess: [],
        xiaoshuocontent: [],
        xiangshengcontent: [],
        tuokocontent: []
			}
		},
		onLoad() {
      this.getData();
		},
		methods: {
      async getData() {
        try{
          const { data } = await this.myRequest({
            url: 'http://mobile.ximalaya.com/mobile/discovery/v3/recommend/hotAndGuess?code=43_310000_3100&device=android&version=5.4.45'
          });
          
          console.log('res: ',data)
          
          if (data.ret == 1) {
            this.showitem = false;
            return;
          }
          
          this.guess = data.paidArea.list
          this.xiaoshuocontent = data.hotRecommends.list[0].list
          this.xiangshengcontent = data.hotRecommends.list[2].list
          this.tuokocontent = data.hotRecommends.list[4].list
        } catch(err) {
          console.log(err);
          this.showitem = false;
          return;
        }
        
      },
      //轮播图改变事件
      swiperChange(e) {
        this.swiperCurrent = e.detail.current
      },
      goToBangDan() {
        uni.navigateTo({
          url: '/pages/index/bangdan/index'
        })
      },
      gotoDetails(e) {
        var url = e.currentTarget.dataset.coverimg;
        var title = e.currentTarget.dataset.title;
        uni.navigateTo({
          url: '/pages/details/index?url=' + url + '&title=' + title,
        })
      }
		},
    filters: {
      pc (val) {
        let value = val * 1 || 0;
        return value;
      }
    }
	}
</script>

<style lang="scss" scoped>
/* 宫格导航 */
.hmly-nav{
  width: 90%;
  height: 132rpx;
  margin: 0rpx auto;
  margin-top: 40rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
  align-content: center;
}
.hmly-nav-item{
  width: 94rpx;
  font-size: 20rpx;
  text-align: center;
  line-height: 35rpx;
  color: #aaa;
}
.hmly-nav-icon{
  width: 84rpx;
  height: 84rpx;
}
/* 猜你喜欢 */
.hmly-like{
  width: 90%;
  margin: 0rpx auto;
  margin-top: 40rpx;
}
.hmly-like-item-box{
  width: 100%;
  display: flex;
  justify-content: space-between;
  overflow: hidden;
}
.hmly-like-item{
  width: 210rpx;
  height: 310rpx;
  border-radius: 15rpx;
}
.hmly-like-img{
  width: 210rpx;
  height: 210rpx;
  border-radius: 15rpx;
  position: relative;
}
.hmly-like-item-icon{
  width: 100%;
  height: 100%;
  border-radius: 15rpx;
}
.hmly-like-text{
  font-size: 28rpx;
  color: #333;
  margin-top: 10rpx;
  display: -webkit-box;
  -webkit-line-clamp: 2;/*行数n*/
  -webkit-box-orient: vertical; 
  overflow: hidden;
  text-overflow: ellipsis;
}
.hmly-like-cover{
  width: 190rpx;
  height: 40rpx;
  /* 透明背景层 */
  background-image: linear-gradient(rgba(0, 0, 0, 0.01), rgba(0, 0, 0, 1));
  /* opacity: 0.3; */
  position: absolute;
  bottom: 0rpx;
  color: #fff;
  font-size: 25rpx;
  padding: 5rpx 10rpx;
  border-bottom-left-radius: 15rpx;
  border-bottom-right-radius: 15rpx;
}
.hmly-data-notip{
  width: 100%;
  height: 300rpx;
  padding-top: 150rpx;
}
.hmly-tip{
  width: auto;
  height: 100rpx;
  text-align: center;
  margin: 0rpx auto;
  color: red;
  font-weight: 800;
}
</style>
