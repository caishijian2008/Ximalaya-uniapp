<template>
	<view>
		<view class="hmly-main bg-white" :style="{'min-height': height + 'px'}">
		    <view class="hmly-content_">
		        <!-- 提示标语 -->
		        <view class="hmly-slogn">
		            <!-- <view class="left-line" style="width:20rpx"></view> -->
		            登录后即可收听你的收藏专辑哦
		            <!-- <view class="right-line" style="width:20rpx"></view> -->
		        </view>
		        <!-- 表单输入部分 -->
		        <view class="hmly-login">
		            <form class="frombox" report-submit="false" bindsubmit="" bindreset="">
		                <!-- 输入手机号 -->
		                <view class="hmly-phone-number">
		                    <view class="hmly-code">+86</view>
		                    <input type="number" placeholder="请输入手机号" placeholder-class="hmly-place"></input>
		                </view>      
		                <!-- 验证码 -->
		                <view class="hmly-yzm">
		                    <input type="number" placeholder="输入验证码" placeholder-class="hmly-place"></input>
		                    <view class="hmly-get-code">获取验证码</view>
		                </view>
		                <view class="hmly-submit" @tap="login">
		                    <button><text class="icon-wechat"></text> 立即登录</button>
		                </view>
		            </form>
		        </view>
		        <!-- 其他登录方式 -->
		        <view class="hmly-wechat" >
		            <view class="hmly-tips" >
		                <view class="hmly-left-line"></view>
		                其他账户登录
		                <view class="hmly-right-line"></view>
		            </view>
		            <view class="hmly-wecaht-login" >
		                <button><text class="icon-wechat"></text> 微信登陆</button>
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
				height:400
			};
		},
    onLoad() {
      uni.getSystemInfo({
        success: (res) => {
          console.log(res.windowHeight)
          this.height = res.windowHeight
        }
      })
    },
    methods: {
      login() {
        uni.showToast({
          title: '成功'
        })
      }
    }
	}
</script>

<style lang="scss" scoped>
/*  
    96D655 
    CCCCCC
*/
.hmly-main{
   width: 100%; 
}

.hmly-content_{
    width: 80%;
    margin: 0rpx auto;
    margin-top: 100rpx;
    display: flex;
    flex-wrap: wrap
}
.hmly-slogn{
    width: 100%;
    height: auto;
    font-size: 25rpx;
    color: #c3c3c3;
    text-align: center;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}
.hmly-login{
    width: 100%;
    height: auto;
    margin-top: 50rpx;
    overflow: hidden;
}
.hmly-phone-number{
    width: 100%;
    height: auto;
    display: flex;
    padding: 20rpx;
    justify-content: flex-start;
    align-items: center;
    border-bottom: 0.5rpx solid #cccccc;
}
.hmly-code{
    width: 60rpx;
    font-size: 27rpx;
    line-height: 60rpx;
    text-align: center;
    padding-right: 20rpx;
    border-right: 1rpx solid #cccccc;
    margin-right: 20rpx;
    color: #cccccc;
}
.hmly-yzm{
    width: 100%;
    height: auto;
    display: flex;
    padding: 20rpx;
    justify-content: flex-start;
    align-items: center;
    box-sizing: border-box;
    border-bottom: 0.5rpx solid #cccccc;
}
.hmly-get-code{
    width: 200rpx;
    font-size: 35rpx;
    line-height: 60rpx;
    text-align: center;
    padding-left: 20rpx;
    border-left: 1rpx solid #cccccc;
    /* box-sizing: border-box; */
    /* margin-left: 20rpx; */
    color: #cccccc;
}
.hmly-place{
    font-size: 29rpx;
}
.hmly-submit{
    width: 100%;
    height: 100rpx;
    margin-top: 50rpx;
    border-radius: 50rpx;
    border: 0rpx;
}
.hmly-submit button{
    width: 100%;
    height: 100rpx;
    /* margin-top: 50rpx; */
    border-radius: 50rpx;
    border: 0rpx;
    color: #ffffff;
    background: #cccccc;
    font-size: 38rpx;
}
.hmly-wechat{
    width: 100%;
    height: auto;
    margin-top: 150rpx;
    text-align: center;
}
.hmly-tips{
    font-size: 32rpx;
    color: #333333;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}
.hmly-left-line{
    width: 100rpx;
    height: 3rpx;
    background: #aaa;
}
.hmly-right-line{
    width: 100rpx;
    height: 3rpx;
    background: #aaa;
}
.hmly-wecaht-login{
    width: 100%;
    height: 100rpx;
    margin-top: 100rpx;
    border-radius: 50rpx;
    border: 0rpx;
}
.hmly-wecaht-login button{
    width: 100%;
    height: 100rpx;
    border-radius: 50rpx;
    border: 0rpx;
    background: #96D655;
    color: #ffffff;
    font-size: 38rpx;
}
</style>
