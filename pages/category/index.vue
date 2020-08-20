<template>
	<view>
		<!-- 搜索框 -->
		<mysearch></mysearch>
    
    <!-- 分类索引 -->
    <view class="hmly-ification">
        <!-- 左边部分 -->
        <scroll-view class="hmly-scroll-left" scroll-y scroll-with-animation :style="{height:phoneHeight + 'rpx'}" :scroll-top="VerticalNavTop">
            <block v-for="(item, index) in ificationTitle" :key="index">
                <view :class="['hmly-left-title', index === activeIndex ? 'hmly-active':'']" :data-index="index" :data-id="index" @tap="changeIt">{{item.title}}</view>
            </block>
        </scroll-view>
        
        <!-- 右边部分 -->
        
        <scroll-view class="hmly-scroll-right" scroll-y @scroll="showActive" :style="{height:phoneHeight +'rpx'}" :scroll-into-view="'main-id-'+TabCur">
            <view class="hmly-content-scroll-item" v-for="(item, index) in ificationContent" :key="index" :data-index="index" :id="'main-id-'+index">
                <view class="hmly-top">
                    <view class="hmly-content-title">
                        {{item.title}}
                        <text class="icon-right"></text>
                    </view>
                </view>
                <view class="hmly-content">
                    <view class="hmly-content-text" v-for="(subitem,index) in item.content" :key="index">
                        {{subitem.text}}
                    </view>
                </view>
            </view>
        </scroll-view>
    </view>
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
				activeIndex:0,
				VerticalNavTop: 0,
				TabCur: 0,
				ificationTitle:[
				  {title:"有声书"},
				  {title:"畅销书"},
				  {title:"儿童"},
				  {title:"相声评书"},
				  {title:"情感生活"},
				  {title:"人文"},
				  {title:"历史"},
				  {title:"国学书院"},
				  {title:"音乐"},
				  {title:"英语"},
				  {title:"教育培训"},
				  {title:"健康养生"},
				  {title:"广播剧"},
				  {title:"戏曲"}
				],
				ificationContent:[
				  {
				    title:"有声书",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"畅销书",
				    content:[
				      {text:"社科"},
				      {text:"经管"},
				      {text:"文学"},
				      {text:"励志"},
				      {text:"名著"},
				      {text:"生活"}
				    ]
				  },
				  {
				    title:"儿童",
				    content:[
				      {text:"故事"},
				      {text:"儿歌"},
				      {text:"动画"},
				      {text:"科普"},
				      {text:"名著"},
				      {text:"国学"}
				    ]
				  },
				  {
				    title:"相声评书",
				    content:[
				      {text:"单田芳"},
				      {text:"郭德纲"},
				      {text:"热门相声"},
				      {text:"单口相声"},
				      {text:"名家评书"},
				      {text:"新锐笑将"}
				    ]
				  },
				  {
				    title:"情感生活",
				    content:[
				      {text:"恋爱技巧"},
				      {text:"睡前夜话"},
				      {text:"情绪压力"},
				      {text:"婚姻家庭"},
				      {text:"个人成长"},
				      {text:"心理健康"}
				    ]
				  },
				  {
				    title:"人文",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"历史",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"国学书院",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"音乐",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"英语",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"教育培训",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"健康养生",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"广播剧",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ]
				  },
				  {
				    title:"戏曲",
				    content:[
				      {text:"言情"},
				      {text:"悬疑"},
				      {text:"都市"},
				      {text:"幻想"},
				      {text:"武侠"},
				      {text:"历史"}
				    ],
				  },
				],
        phoneHeight: 0
			};
		},
    onLoad() {
      uni.getSystemInfo({
        success: (res) => {
          console.log('res==: ',res)
          let height = res.windowHeight*2
          this.phoneHeight = height
        }
      })
    },
    methods: {
      showActive(e) {
        let index = parseInt( e.detail.scrollTop/116);
        this.activeIndex = index
      },
      changeIt(e) {
        this.VerticalNavTop = (e.currentTarget.dataset.index - 1) * 50
        this.activeIndex = e.currentTarget.dataset.index
        this.TabCur = e.currentTarget.dataset.id
      }
    },
	}
</script>

<style lang="scss" scoped>
.hmly-ification{
    width: 100%;
    height: 100%;
    
    background-color: rgb(243, 244, 246);
    display: flex;
    justify-content: start;
}
.hmly-scroll-left{
    width: 22%;
    padding-top: 55rpx;
    margin-right: 20rpx;
    background-color: #fff;
    overflow: hidden;
}
.hmly-left-title{
    text-align: center;
    font-size: 28rpx;
    height: 100rpx;
    line-height: 100rpx;
}

.hmly-scroll-right{
    width: 75%;
}
.hmly-active{
    color: #ff520f;
    background-color: rgb(243, 244, 246);
}
.hmly-content-scroll-item{
    width: auto;
    height: auto;
    margin-bottom: 20rpx;
}
.hmly-top{
    width: 100%;
    height: 40rpx;
    padding: 20rpx 0rpx;
    margin: 0rpx auto;
}
.hmly-content-title{
    color: rgb(12, 11, 11);
    font-size: 30rpx;
    text-align: center;
    // margin: 0rpx auto;
    display: block;
}
.hmly-content{
    width: 100%;
    height: 140rpx;
    padding: 30rpx 0rpx;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: space-around;
    justify-content: space-between;
    background-color: #fff;
    border-top-left-radius: 7rpx;
    border-bottom-left-radius: 7rpx;
}
.hmly-content-text{
    width: 130rpx;
    height: 50rpx;
    margin: 10rpx 20rpx;
    font-size: 30rpx;
    text-align: center;
}
</style>
