<template name="basics">
	<view>
		<scroll-view scroll-y class="page">
			<image src="/static/BasicsBg.png" mode="widthFix" class="response"></image>
			<!-- <swiper class="card-swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="true" :circular="true"
			 :autoplay="true" interval="5000" duration="500" @change="cardSwiper" indicator-color="#8799a3"
			 indicator-active-color="#0081ff">
				<swiper-item v-for="(item,index) in swiperList" :key="index" :class="cardCur==index?'cur':''">
					<view class="swiper-item">
						<image :src="item.url" mode="aspectFill" v-if="item.type=='image'"></image>
						<video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type=='video'"></video>
					</view>
				</swiper-item>
			</swiper> -->
			<!-- <swiper class="screen-swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="true" :circular="true"
			 :autoplay="true" interval="5000" duration="500">
				<swiper-item v-for="(item,index) in swiperList" :key="index">
					<image :src="item.url" mode="aspectFill" v-if="item.type=='image'"></image>
					<video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type=='video'"></video>
				</swiper-item>
			</swiper> -->
			<view class="nav-list" style="margin-top: 20px;">
				<navigator hover-class="none" :url="'/pages/toub/' + item.name" class="nav-li" navigateTo :class="'bg-'+item.color"
				 :style="[{animation: 'show ' + ((index+1)*0.2+1) + 's 1'}]" v-for="(item,index) in elements" :key="index">
					<view class="nav-title">{{item.title}}</view>
					<view class="nav-name">{{item.name}}</view>
					<text :class="'cuIcon-' + item.cuIcon"></text>
				</navigator>
			</view>
			<view class="cu-tabbar-height"></view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		name: "basics",
		data() {
			return {
				elements: [{
						title: '网上申报',
						name: 'declaration',
						color: 'cyan',
						cuIcon: 'newsfill'
					},
					{
						title: '办件查询',
						name: 'query',
						color: 'blue',
						cuIcon: 'colorlens'
					},
					{
						title: '证件上传',
						name: 'credentials',
						color: 'purple',
						cuIcon: 'font'
					},
					{
						title: '我的办件',
						name: 'toDoList',
						color: 'mauve',
						cuIcon: 'cuIcon'
					},
					{
						title: '消息提醒',
						name: 'messageAlert',
						color: 'pink',
						cuIcon: 'btn'
					},
					{
						title: '我的EMS',
						name: 'myEMS',
						color: 'brown',
						cuIcon: 'tagfill'
					},
					{
						title: '用户评价',
						name: 'userRating',
						color: 'red',
						cuIcon: 'myfill'
					},
					{
						title: '智能问答',
						name: 'smartQA',
						color: 'orange',
						cuIcon: 'icloading'
					},
					
					
					
					
					// {
					// 	title: '布局',
					// 	name: 'layout',
					// 	color: 'cyan',
					// 	cuIcon: 'newsfill'
					// },
					// {
					// 	title: '背景',
					// 	name: 'background',
					// 	color: 'blue',
					// 	cuIcon: 'colorlens'
					// },
					// {
					// 	title: '文本',
					// 	name: 'text',
					// 	color: 'purple',
					// 	cuIcon: 'font'
					// },
					// {
					// 	title: '图标 ',
					// 	name: 'icon',
					// 	color: 'mauve',
					// 	cuIcon: 'cuIcon'
					// },
					// {
					// 	title: '按钮',
					// 	name: 'button',
					// 	color: 'pink',
					// 	cuIcon: 'btn'
					// },
					// {
					// 	title: '标签',
					// 	name: 'tag',
					// 	color: 'brown',
					// 	cuIcon: 'tagfill'
					// },
					// {
					// 	title: '头像',
					// 	name: 'avatar',
					// 	color: 'red',
					// 	cuIcon: 'myfill'
					// },
					// {
					// 	title: '进度条',
					// 	name: 'progress',
					// 	color: 'orange',
					// 	cuIcon: 'icloading'
					// },
					// {
					// 	title: '边框阴影',
					// 	name: 'shadow',
					// 	color: 'olive',
					// 	cuIcon: 'copy'
					// },
					// {
					// 	title: '加载',
					// 	name: 'loading',
					// 	color: 'green',
					// 	cuIcon: 'loading2'
					// }
				],
				swiperList: [{
					id: 0,
					type: 'image',
					url: '../../static/index/hutcjdq.png'
				}, {
					id: 1,
					type: 'image',
					url: '../../static/index/xtgjtd.png',
				}, {
					id: 2,
					type: 'image',
					url: '../../static/index/yd.png'
				}, {
					id: 3,
					type: 'image',
					url: '../../static/index/yihryye.png'
				}],
				cardCur: 0,
				dotStyle: false,
				towerStart: 0,
				direction: ''
			};
		},
		onShow() {
			console.log("success")
		},
		methods: {
			DotStyle(e) {
				this.dotStyle = e.detail.value
			},
			// cardSwiper
			cardSwiper(e) {
				this.cardCur = e.detail.current
			},
			// towerSwiper
			// 初始化towerSwiper
			TowerSwiper(name) {
				let list = this[name];
				for (let i = 0; i < list.length; i++) {
					list[i].zIndex = parseInt(list.length / 2) + 1 - Math.abs(i - parseInt(list.length / 2))
					list[i].mLeft = i - parseInt(list.length / 2)
				}
				this.swiperList = list
			},
			// towerSwiper触摸开始
			TowerStart(e) {
				this.towerStart = e.touches[0].pageX
			},
			
			// towerSwiper计算方向
			TowerMove(e) {
				this.direction = e.touches[0].pageX - this.towerStart > 0 ? 'right' : 'left'
			},
			
			// towerSwiper计算滚动
			TowerEnd(e) {
				let direction = this.direction;
				let list = this.swiperList;
				if (direction == 'right') {
					let mLeft = list[0].mLeft;
					let zIndex = list[0].zIndex;
					for (let i = 1; i < this.swiperList.length; i++) {
						this.swiperList[i - 1].mLeft = this.swiperList[i].mLeft
						this.swiperList[i - 1].zIndex = this.swiperList[i].zIndex
					}
					this.swiperList[list.length - 1].mLeft = mLeft;
					this.swiperList[list.length - 1].zIndex = zIndex;
				} else {
					let mLeft = list[list.length - 1].mLeft;
					let zIndex = list[list.length - 1].zIndex;
					for (let i = this.swiperList.length - 1; i > 0; i--) {
						this.swiperList[i].mLeft = this.swiperList[i - 1].mLeft
						this.swiperList[i].zIndex = this.swiperList[i - 1].zIndex
					}
					this.swiperList[0].mLeft = mLeft;
					this.swiperList[0].zIndex = zIndex;
				}
				this.direction = ""
				this.swiperList = this.swiperList
			},
		}
	}
</script>

<style>
	.page {
		height: 100vh;
	}
	.tower-swiper .tower-item {
		transform: scale(calc(0.5 + var(--index) / 10));
		margin-left: calc(var(--left) * 100upx - 150upx);
		z-index: var(--index);
	}
</style>
