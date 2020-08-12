<template>
	<view>
		<!-- 搜索框 -->
		<view class="hmly-search">
			<view class="hmly-search-left">
				<text class="icon-search"></text>
				<input placeholder="搜索你想听的节目"></input>
			</view>
			<view class="hmly-search-right">取消</view>
		</view>
		<!-- 搜索历史 -->
		<view class="hmly-history">
			<!-- 提示标题 -->
			<view class="hmly-title">
				<view class="hmly-title-text">搜索历史</view>
				<text class="icon-delete text-gray"></text>
			</view>
			<!-- 内容 -->
			<view class="hmly-history-content">
				<view class="hmly-content-item bg-gray text-black">庆余年</view>
				<view class="hmly-content-item bg-gray text-black">德云社</view>
				<view class="hmly-content-item bg-gray text-black">评书</view>
				<view class="hmly-content-item bg-gray text-black">英语</view>
			</view>
		</view>
		<!-- 热门搜索 -->
		<view class="hmly-hot">
			<!-- 提示标题 -->
			<view class="hmly-title">
				<view class="title-text">热门搜索</view>
			</view>
			<view class="hmly-hot-content">
				<view class="hmly-hot-items" v-for="(item, index) in hotData" :key="index">
					<view class="hmly-item-left">
						<view :class="[index < 3 ? 'text-red' : '']">{{index + 1}}</view>
						<view class="hmly-item-title text-black">{{item.title}}</view>
					</view>
					<text :class="[item.icon, item.color]"></text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				hotData:[
				  {title:"宝宝巴士",icon:"icon-jiantouUp",color:"text-orange"},
				  {title:"孟鹤堂",icon:"icon-jiantouUp",color:"text-red"},
				  {title:"三体",icon:"icon-jiantouDown",color:"text-green"},
				  {title:"龙王殿",icon:"icon-jiantouUp",color:"text-red"},
				  {title:"儿童恐龙故事",icon:"icon-jiantouDown",color:"text-red"},
				  {title:"儿童版三国演义",icon:"icon-jiantouUp",color:"text-red"},
				]
			};
		}
	}
</script>

<style lang="scss" scoped>
/* 
  ======== 
  搜索部分css 
  ========
*/
.hmly-search{
  width: 90%;
  height: auto;
  display: flex;
  align-items: center;
  margin: 0rpx auto;
}

.hmly-search-left{
  flex: 4;
  background-color: rgb(240, 240, 240);
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding: 10rpx 20rpx;
  border-radius: 15rpx;
}

.hmly-search input{
  width: 90%;
  height: 100%;
  font-size: 29rpx;
  margin-left: 20rpx;
}
.hmly-search-right{
  flex: 0.5;
  font-size:30rpx;
  color: #aaa;
  text-align: center;
  margin-left: 30rpx;
}
/* 
  ======== 
  搜索历史和热门搜索部分css 
  ========
*/
.hmly-title{
  width: 100%;
  height: 50rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-sizing: border-box;
}
.hmly-title-text{
  color: #000;
  font-weight: 700;
}
.hmly-history{
  width: 90%;
  height: auto;
  margin: 0rpx auto;
  margin-top: 80rpx;
}
.hmly-history-content{
  width: 100%;
  height: auto;
  margin-top: 30rpx;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  align-items: center;
}
.hmly-content-item{
  width: 150rpx;
  font-size: 33rpx;
  text-align: center;
  padding: 10rpx 20rpx;
  margin-bottom: 20rpx;
  border-radius: 25rpx;
}

.hmly-hot{
  width: 90%;
  height: auto;
  margin: 0rpx auto;
  margin-top: 80rpx;
}
.hmly-hot-content{
  width: 100%;
  height: auto;
  margin-top: 30rpx;
}
.hmly-hot-items{
  width: 100%;
  height: 50rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20rpx;
}
.hmly-item-left{
  display: flex;
  justify-content: flex-start;
  font-size: 32rpx;
}
.hmly-item-title{
  margin-left: 40rpx;
}
</style>
