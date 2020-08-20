<template>
	<view class="search marginTopBottom" @tap="goToSearch">
		<view class="search-left">
			<text class="icon-search"></text>
			<input placeholder="搜索你想听的节目" :disabled="disabled"></input>
		</view>
		<view class="search-right" v-if="isshow">取消</view>
	</view>
</template>

<script>
	export default {
    props: {
      myProperty:{
          type: String,
          value: ''
      },
    },
		data() {
			return {
				disabled: true,
				isshow: false,
			};
		},
    methods: {
      goToSearch(){
          uni.navigateTo({
            url: '../../pages/search/index',
          })
      }
    },
	}
</script>

<style lang="scss">
.search{
  width: 90%;
  height: auto;
  display: flex;
  align-items: center;
  margin: 0rpx auto;
  margin-bottom: 15rpx;
}

.search-left{
  flex: 4;
  background-color: rgb(240, 240, 240);
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding: 10rpx 20rpx;
  border-radius: 15rpx;
}

.search input{
  width: 90%;
  height: 100%;
  font-size: 29rpx;
  margin-left: 20rpx;
}

.search-right{
  flex: 0.5;
  font-size:30rpx;
  color: #aaa;
  text-align: center;
  margin-left: 30rpx;
}
</style>
