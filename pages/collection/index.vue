<template>
  <view>
    <!-- 若是没有登录就显示登录界面 -->
    <block v-if="login">
      <!-- logo -->
      <view class="hmly-logo" hover-class="none" hover-stop-propagation="false">
        <image class="hmly-logo-img" src="../../static/logo.png" mode="widthFix" lazy-load="false"></image>
      </view>
      <!-- 登录按钮 -->
      <view class="hmly-login-button" hover-class="none" hover-stop-propagation="false">
        <view class="hmly-wechat-login">
          <button open-type="getUserInfo" @tap="bindGetUserInfo">
            <text class="icon-message"></text> 微信登录
          </button>
        </view>
        <view class="hmly-phone-login">
          <button>手机号登录</button>
        </view>
      </view>
    </block>
    <block v-else>
      <!-- 搜索框 -->
      <mysearch></mysearch>
      <!-- 功能栏 -->
      <view class="hmly-title-bar">
        <view :class="['hmly-item-title', index == currentIndex ? 'hmly-active' : '']" :data-index="index" 
          @tap="checkItem"
          v-for="(item, index) in content" :key="index">
          {{item.text}}
        </view>
      </view>
      <swiper class="hmly-swiper-box" :style="{'min-height': height + 'px'}" duration="300" :current="currentIndex" @change="changeTab">
        <swiper-item class="hmly-swiper-box-item">
          <block>
            <view class="hmly-no-content">
              <text class="icon-empty text-gray" style="font-size:400rpx"></text>
              <!-- <image src="/image/noContent.png"></image> -->
              <view class="hmly-but-box">
                <text style="font-size:30rpx" class="text-gray">没有内容</text>
                <button class="hmly-but">看看推荐</button>
              </view>
            </view>
          </block>
        </swiper-item>
        <swiper-item>
          <block>
            <view class="hmly-no-content">
              <text class="icon-empty text-gray" style="font-size:400rpx"></text>
              <view class="hmly-but-box">
                <text style="font-size:30rpx" class="text-gray">没有内容</text>
                <button class="hmly-but">看看推荐</button>
              </view>
            </view>
          </block>
        </swiper-item>
        <swiper-item>
          <block>
            <view class="hmly-no-content">
              <text class="icon-empty text-gray" style="font-size:400rpx"></text>
              <view class="hmly-but-box">
                <text style="font-size:30rpx" class="text-gray">没有内容</text>
                <button class="hmly-but">看看推荐</button>
              </view>
            </view>
          </block>
        </swiper-item>
        <swiper-item>
          <block>
            <view class="hmly-no-content">
              <text class="icon-empty text-gray" style="font-size:400rpx"></text>
              <view class="hmly-but-box">
                <text style="font-size:30rpx" class="text-gray">没有内容</text>
                <button class="hmly-but">更多礼包</button>
              </view>
            </view>
          </block>
        </swiper-item>
      </swiper>
    </block>
  </view>
</template>

<script>
  import mysearch from '../../component/search/index.vue'
  export default {
    components: {
      mysearch
    },
    data() {
      return {
        currentIndex:0,
        height: getApp().globalData.phoneHeight,
        content: [
          {text: "我的收藏"},
          {text: "我的已购"},
          {text: "收听历史"},
          {text: "我的礼包"}
        ],
        login: true
      };
    },
    onLoad() {
      let height = 0;
      uni.getSystemInfo({
        success: (res) => {
          console.log(res.windowHeight)
          height = res.windowHeight
        }
      });
      if(getApp().globalData.userInfo === null) {
        this.login = true
      } else {
        this.login = false
        this.height = height
      }
    },
    methods: {
      bindGetUserInfo(e) {
        uni.getUserInfo({
          success: (res) => {
            console.log(e.detail.userInfo)
            getApp().globalData.userInfo = e.detail.userInfo
            this.login = false
          }
        })
      },
      checkItem(e) {
        if(this.data.currentIndex === e.target.dataset.current) {
          return false;
        } else {
          this.currentIndex = e.target.dataset.index
        }
      },
      // 滑动切换tab
      changeTab(e) {
        console.log(e.detail.current)
        this.currentIndex = e.detail.current
      }
    },
  }
</script>

<style lang="scss" scoped>
  .hmly-title-bar {
    width: 100%;
    height: 80rpx;
    /* 这个配色不对 */
    border-bottom: 1rpx solid #f1f1f1;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 28rpx;
    overflow: hidden;
  }

  .hmly-item-title {
    width: 200rpx;
    height: 100%;
    text-align: center;
    line-height: 80rpx;
    position: relative;
    color: #aaa;
  }

  .hmly-active:after {
    content: '';
    width: 40rpx;
    height: 8rpx;
    position: absolute;
    bottom: 0rpx;
    left: 70rpx;
    border-radius: 15rpx;
    background: #ff520f;
  }

  .hmly-active {
    font-size: 32rpx;
    font-weight: 700;
    transition: all 0.3s;
    color: #333;
  }

  .hmly-collection-content {
    width: 90%;
    margin: 0rpx auto;
    margin-top: 10rpx;
  }

  .hmly-collection-content {
    width: 100%;
    text-align: center;
    position: absolute;
    top: 300rpx;
    color: #aaaaaa
  }

  swiper {
    display: block;
    width: 100%;
  }

  .hmly-swiper-box-item {
    height: 400rpx;
  }

  .hmly-no-content {
    width: 90%;
    height: auto;
    margin: 0rpx auto;
    margin-top: 100rpx;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  .hmly-no-content image {
    width: 400rpx;
    height: 300rpx;
    align-self: center;
  }

  .hmly-but-box {
    width: 80%;
    margin: 0rpx auto;
    margin-top: 40rpx;
    text-align: center;
  }

  .hmly-but {
    width: 300rpx;
    height: 80rpx;
    font-size: 40rpx;
    line-height: 80rpx;
    margin-top: 10rpx;
  }
</style>
