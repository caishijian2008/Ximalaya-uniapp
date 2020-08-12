<template>
	<view>
		<!--
		  title和背景 
		  注：这部分的背景色还没有处理好
		-->
		<view class="hmly-top-title-bar">
		    <!-- 背景虚化层 -->
		    <view class="hmly-bg" :style="{background: 'url('+imgurl+')', backgroundSize: '100% 100%', backgroundRepeat: 'no-repeat'}"></view>
		    <!-- 内容 -->
		    <view class="hmly-bar-item" v-for="(item, index) in performanceInfo" :key="index">
		      <view class="hmly-bar-item-top">
		        <view class="hmly-theme-bg-img" :style="{background:'url('+item.imgurl+')', backgroundSize: '100% 100%'}"></view>
		        <view class="hmly-theme-info">
		          <view class="hmly-theme-title">{{item.title}}</view>
		          <view class="hmly-theme-author">
		            <!-- <image class="" src="" mode="widthFix"></image> -->
		            {{item.author}} <text class="icon-right"></text>
		          </view>
		          <view class="hmly-view-info">
		            <view class="hmly-view-info-left">{{item.num1}}人收藏</view>
		            <text class="hmly-viewhmly-info-mid">|</text>
		            <view class="hmly-view-info-right">已更新{{item.num2}}期</view>
		          </view>
		        </view>
		      </view>
		      <view class="hmly-bar-item-bottom">
		        <button class="hmly-share-but"><text class="icon-share"></text> 分享</button>
		        <button class="hmly-collection"><text class="icon-add"></text> 收藏</button>
		      </view>
		    </view>
		</view>
		<!-- 顶部选项 -->
		<view class="hmly-performance">
		  <view class="hmly-selectbar">
		    <view class="hmly-detail">详情</view>
		    <view class="hmly-list hmly-active">节目<text>152</text>
		    </view>
		  </view>
		  <!-- 播放选项 -->
		  <view class="hmly-play">
		    <view class="hmly-play-all">
		      <text class="icon-video"></text> 播放全部
		    </view>
		    <view class="hmly-play-select">
		      <view style="margin-right:20rpx"><text class="icon-order"></text> 正序</view>
		      <view><text class="icon-list"></text> 选集</view>
		    </view>
		  </view>
		  <!-- 节目列表 -->
		  <view class="hmly-performance-content" v-for="(item, index) in performance" :key="index">
		    <!-- 序号 -->
		    <view class="hmly-performance-index">{{index+1}}</view>
		    <!-- 节目标题 -->
		    <view class="hmly-performance-info">
		      <view class="hmly-performance-info-top">
		        <view style="font-size:33rpx">{{item.name}}</view>
		        <view style="color:#aaaaaa">{{item.year}}</view>
		      </view>
		      <!-- 播放次数和时间 -->
		      <view class="hmly-performance-info-bottom">
		        <view><text class="icon-video"></text>{{item.count}}</view>
		        <view style="margin-left:20rpx"><text class="icon-time"></text>{{item.time}}</view>
		      </view>
		    </view>
		  </view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				performance: [{
				    name: "《人在江湖》郭德纲 于谦",
				    year: "2年前",
				    count: "5601.9万",
				    time: "34:36"
				  },
				  {
				    name: "《人在江湖》郭德纲 于谦",
				    year: "2年前",
				    count: "5601.9万",
				    time: "34:36"
				  },
				  {
				    name: "《人在江湖》郭德纲 于谦",
				    year: "2年前",
				    count: "5601.9万",
				    time: "34:36"
				  },
				  {
				    name: "《人在江湖》郭德纲 于谦",
				    year: "2年前",
				    count: "5601.9万",
				    time: "34:36"
				  },
				  {
				    name: "《人在江湖》郭德纲 于谦",
				    year: "2年前",
				    count: "5601.9万",
				    time: "34:36"
				  },
				  {
				    name: "《人在江湖》郭德纲 于谦",
				    year: "2年前",
				    count: "5601.9万",
				    time: "34:36"
				  },
				  {
				    name: "《人在江湖》郭德纲 于谦",
				    year: "2年前",
				    count: "5601.9万",
				    time: "34:36"
				  },
				  {
				    name: "《人在江湖》郭德纲 于谦",
				    year: "2年前",
				    count: "5601.9万",
				    time: "34:36"
				  },
				],
        performanceInfo: [],
        imgurl: ''
			};
		},
    onLoad(options) {
      console.log('options: ',options)
      this.performanceInfo = [{
        imgurl: options.url+'=5&upload_type=album&device_type=ios&name=medium&magick=png',
        title: options.title,
        author: "某某某",
        num1: "767.6万",
        num2: "257"
      }];
      this.imgurl = options.url+'=5&upload_type=album&device_type=ios&name=medium&magick=png'
    }
	}
</script>

<style lang="scss" scoped>
.hmly-top-title-bar {
  width: 100%;
  height: 410rpx;
  overflow: hidden;
  position: relative;
}
/* 背景虚化层 */
.hmly-bg{
  width: 100%;
  height: 410rpx;
  filter: blur(15rpx);
}
.hmly-bar-item {
  width: 100%;
  height: 400rpx;
  margin-top: 50rpx;
  padding: 20rpx 0rpx;
  position: absolute;
  top: 0rpx;
}

.hmly-bar-item-top {
  width: 100%;
  height: 200rpx;
  display: flex;
  justify-content: center;
  align-items: center;
}

.hmly-theme-bg-img {
  width: 200rpx;
  height: 200rpx;
  margin-right: 30rpx;
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.hmly-theme-info {
  width: 60%;
  height: 200rpx;
}

.hmly-theme-title {
  color: #fff;
  font-size: 40rpx;
  display: -webkit-box;
  -webkit-line-clamp: 2;/*行数n*/
  -webkit-box-orient: vertical; 
  overflow: hidden;
  text-overflow: ellipsis;
}

.hmly-theme-author {
  font-size: 25rpx;
  color: #fff;
  margin-top: 5rpx;
}

.hmly-view-info {
  color: #fff;
  font-size: 30rpx;
  margin-top: 5rpx;
  display: flex;
  justify-content: flex-start;
}

.hmly-view-info-left {
  margin-right: 5rpx;
}

.hmly-view-info-right {
  margin-left: 5rpx;
}

.hmly-bar-item-bottom {
  width: 70%;
  height: 100rpx;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  border-radius: 20rpx;
  float: right;
  margin-top: 15rpx;
}

.hmly-bar-item-bottom button {
  width: 210rpx;
  height: 75rpx;
  text-align: center;
  font-size: 30rpx;
  color: #fff;
  border-radius: 20rpx;
}

.hmly-share-but {
  background: orangered;
  border: 1rpx solid #fff;
  margin-left: 70rpx;
}

.hmly-collection {
  background: orangered;
}

.hmly-performance {
  width: 100%;
  height: 500rpx;
  border-top-left-radius: 20rpx;
  border-top-right-radius: 20rpx;
  position: relative;
  top: -10rpx;
}
.hmly-selectbar {
  width: 100%;
  height: 100rpx;
  line-height: 100rpx;
  text-align: center;
  display: flex;
  justify-content: space-between;
  background: #fff;
  box-sizing: border-box;
  color: #aaa;
  border-radius: 15rpx;
  border-bottom: 1rpx solid #f1f1f1;
}

.hmly-detail {
  width: 50%;
}

.hmly-list {
  width: 50%;
}

.hmly-play {
  width: 100%;
  height: 100rpx;
  padding: 0rpx 40rpx;
  box-sizing: border-box;
  border-bottom: 1rpx solid #f1f1f1;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.hmly-play-all {
  width: auto;
  text-align: center;
  font-size: 30rpx;
}

.hmly-play-select {
  width: auto;
  display: flex;
  justify-content: space-between;
  text-align: center;
  font-size: 30rpx;
}

.hmly-performance-content {
  width: 100%;
  height: 150rpx;
  display: flex;
  box-sizing: border-box;
  justify-content: flex-start;
  align-items: center;
  border-bottom: 1rpx solid #f1f1f1;
  padding: 20rpx 20rpx;
}

.hmly-performance-index {
  width: 15%;
  height: 80rpx;
  text-align: center;
  line-height: 80rpx;
  color: #aaa;
}

.hmly-performance-info {
  width: 85%;
  height: 100%;
}

.hmly-performance-info-top {
  width: 100%;
  height: 50%;
  display: flex;
  justify-content: space-between;
  font-size: 30rpx;
}

.hmly-performance-info-bottom {
  width: 100%;
  height: auto;
  display: flex;
  justify-content: flex-start;
  color: #aaa;
  font-size: 25rpx;
  margin-top: 20rpx;
}
.hmly-active{
  position: relative;
  color: #333;
}
.hmly-active::after{
  content: '';
  width: 80rpx;
  height: 5rpx;
  position: absolute;
  bottom: 0rpx;
  left: 150rpx;
  background-color: orangered;
}
</style>
