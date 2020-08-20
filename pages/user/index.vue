<template>
	<view>
		<block v-if="login">
			<!-- logo -->
			<view class="hmly-logo">
				<image class="hmly-logo-img" src="../../static/logo.png" mode="widthFix"></image>
			</view>
			<!-- 登录按钮 -->
			<view class="hmly-login-button">
				<!-- 在本小程序中只实现了微信登录 -->
				<view class="hmly-wechat-login">
					<button open-type="getUserInfo" @tap="bindGetUserInfo">
						<text class="icon-message"></text> 微信登录
					</button>
				</view>
				<view class="hmly-phone-login" @tap="phoneLogin">
					<button>手机号登录</button>
				</view>
			</view>
		</block>
    <!-- 已经登录显示界面 -->
    <block wx:else>
    	<view class="hmly-body" :style="{height:phoneHeight+'px'}">
    		<!-- 头像昵称签到部分 -->
    		<view class="hmly-top-bar">
    			<!-- 头像昵称 -->
    			<view class="hmly-user-img">
    				<view class="hmly-avatar-nickname">
    					<view class="hmly-avatar">
    						<image class="hmly-avatar-img" :src="avatarUrl"></image>
    					</view>
    					<view class="hmly-nickname">
    						<text class="#">{{nickName}}</text>
    						<!-- vip勋章 -->
    						<text class="icon-vip" style="margin-left:30rpx"></text>
    					</view>
    				</view>
    				<view class="hmly-kefu"><text class="icon-service"></text>客服服务</view>
    			</view>
    			<!-- 签到 -->
    			<view class="hmly-qian-dao">
    				<!-- 签到涉及canvas所以暂时搁置 -->
    				<view class="hmly-qian-text">
    					<text class="icon-dateTable text-gray"></text>
    					<text style="margin-left:20rpx">签到</text>
    				</view>
    				<view class="hmly-icon_">
    					<text class="icon-right text-gray"></text>
    				</view>
    			</view>
    		</view>
    		<!-- 选项卡部分 -->
    		<view class="hmly-chioce">
    			<!-- 选项卡item -->
    			<view class="hmly-choice-item" @tap="openSwitch">
    				<view class="">
    					<text class="icon-time text-gray"></text>
    					<text style="margin-left:20rpx">定时关闭</text>
    				</view>
    				<text class="icon-right text-gray"></text>
    			</view>
    			<view class="hmly-choice-item">
    				<!-- 
    					
    					因为切换为夜间模式需要使用自定义的tarbar，
    				  而这个小程序是一个初级学习项目，所以此功能暂时搁置 
    	
    				-->
    				<view class="">
    					<text class="icon-tip text-gray"></text>
    					<text style="margin-left:20rpx">夜间模式</text>
    				</view>
    				<switch></switch>
    			</view>
    			<view class="hmly-choice-item">
    				<!-- 意见反馈需要使用button的open-type属性 此处没有设置-->
    				<view class="">
    					<text class="icon-write text-gray"></text>
    					<text style="margin-left:20rpx">意见反馈</text>
    				</view>
    				<text class="icon-right text-gray"></text>
    			</view>
    			<view class="hmly-choice-item" @tap="gotoLogin">
    				<view class="">
    					<text class="icon-changeCount text-gray"></text>
    					<text style="margin-left:20rpx">切换账号</text>
    				</view>
    				<text class="icon-right text-gray"></text>
    			</view>
    		</view>
    	</view>
    </block>
    
    <!-- 定时关闭部分 -->
    <block v-if="show">
    	<view class="hmly-switch">
    		<scroll-view class="hmly-scroll-wrapper" scroll-y scroll-with-animation="true" catchtouchmove="preventTouchMove">
    			<view class="hmly-switch-item" v-for="(item, index) in timeout" :key="index" @tap="chooseTimeOut" :data-activeIndex="index">
    				<view>{{item.text}}</view>
    				<view class="hmly-active" v-if="index == activeIndex"></view>
    			</view>
    		</scroll-view>
    		<view class="hmly-close" @tap="close">关闭</view>
    	</view>
    	<view class="hmly-cover"></view>
    </block>
	</view>
</template>

<script>
	export default {
		data() {
			return {
        timeout:[
          {text:"不开启"},
          {text:"播放当前声音关闭"},
          {text:"播放2首声音关闭"},
          {text:"播放3首声音关闭"},
          {text:"播放4首声音关闭"},
          {text:"10分钟后"},
          {text:"20分钟后"},
          {text:"30分钟后"},
        ],
        activeIndex:0,
				login: true,
        phoneHeight: 0,
        avatarUrl: '',
        nickName: '',
        show: false
			};
		},
    onLoad() {
      uni.getSystemInfo({
        // success(res) {
        //   console.log(res.windowHeight)
        // }
        success: (res) => {
          console.log('res.windowHeight: ',res.windowHeight)
          this.phoneHeight = res.windowHeight
        }
      })
      
      console.log('getApp().globalData.userInfo: ',getApp().globalData.userInfo)
      
      if(getApp().globalData.userInfo === null) {
        this.login = true
      } else {
        this.login = false
        this.avatarUrl = getApp().globalData.userInfo.avatarUrl
        this.nickName = getApp().globalData.userInfo.nickName
      }
    },
    methods: {
      bindGetUserInfo(e) {
        uni.getUserInfo({
          success: (res) => {
            console.log('e.detail.userInfo: ',e.detail.userInfo);
            getApp().globalData.userInfo = e.detail.userInfo;
            this.login = false
            this.avatarUrl = e.detail.userInfo.avatarUrl
            this.nickName = e.detail.userInfo.nickName
          }
        })
      },
      phoneLogin() {
        uni.navigateTo({
          url:'./phoneLogin/index'
        })
      },
      gotoLogin() {
        uni.navigateTo({
          url:'./phoneLogin/index'
        })
      },
      openSwitch() {
        this.show = true
      },
      close() {
        this.show = false
      },
      chooseTimeOut(e) {
        this.activeIndex = e.currentTarget.dataset.activeIndex
      }
    },
	}
</script>

<style lang="scss" scoped>
/* pages/user/user.wxss */
.hmly-body {
    background-color: #f1f1f1;
}

.hmly-top-bar {
    width: 100%;
    height: 270rpx;
    background-color: #fff;
}

.hmly-user-img {
    width: 95%;
    height: 200rpx;
    margin: 0rpx auto;
    display: flex;
    justify-content: space-around;
    align-items: center;

}

.hmly-avatar-nickname {
    width: 70%;
    height: 100%;
    display: flex;
    justify-content: start;
    align-items: center;
}

.hmly-avatar {
    width: 120rpx;
    height: 120rpx;
    border-radius: 50%;
}

.hmly-avatar-img {
    width: 120rpx;
    height: 120rpx;
    border-radius: 50%;
}

.hmly-nickname {
    margin-left: 20rpx;
}

.hmly-qian-dao {
    width: 90%;
    height: 70rpx;
    padding: 0rpx 30rpx;
    font-size: 32rpx;
}

.hmly-qian-text {
    float: left;
}

.hmly-icon_ {
    float: right;
}

.hmly-kefu {
    width: 160rpx;
    height: 50rpx;
    font-size: 25rpx;
    border-radius: 25rpx;
    outline: none;
    text-align: center;
    line-height: 50rpx;
    background-color: #f1f1f1;
}

/* 选项卡 */
.hmly-chioce {
    width: 100%;
    height: auto;
    background-color: #fff;
    margin-top: 10rpx;
    font-size: 32rpx;
}

.hmly-choice-item {
    display: flex;
    width: 90%;
    height: 60rpx;
    padding: 20rpx 30rpx;
    justify-content: space-between;
    align-items: center;
}

/* 定时关闭 */
.hmly-switch {
    width: 100%;
    height: 500rpx;
    position: fixed;
    bottom: 0rpx;
    z-index: 9999;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-wrap: wrap;
    background: #fff;
    border-top-left-radius: 15rpx;
    border-top-right-radius: 15rpx;
    padding-top: 20rpx;
}

.hmly-switch-item {
    width: 100%;
    height: 120rpx;
    line-height: 120rpx;
    border-bottom: 1rpx solid #f1f1f1;
    display: flex;
    justify-content: space-between;
    align-items: center;
    /* padding: 0rpx 30rpx; */
}

.hmly-close {
    width: 100%;
    height: 100rpx;
    text-align: center;
    line-height: 100rpx;
}

.hmly-scroll-wrapper {
    white-space: nowrap;
    -webkit-overflow-scrolling: touch;
    background: #FFF;
    padding-left: 20rpx;
    width: 100%;
    height: 400rpx;
    box-sizing: border-box;
}

::-webkit-scrollbar {
    width: 0;
    height: 0;
    color: transparent;
}
.hmly-active{
    width: 30rpx;
    height: 30rpx;
    background-color: red;
    border-radius: 50%;
    margin-right: 40rpx;
}
</style>
