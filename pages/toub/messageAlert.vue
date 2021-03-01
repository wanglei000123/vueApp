<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">消息提醒</block>
		</cu-custom>
		<view class="content">
			<div class="aui-news-box">
				<a href="javascript:;" class="aui-news-item" v-for="(list, i) in lists" :key="i">
					<div class="aui-news-item-hd">
						<img :src="list.img" alt="">
					</div>
					<div class="aui-news-item-bd">
						<h4>{{list.tit1}}</h4>
						<p>{{list.tit2}}</p>
					</div>
					<span class="aui-news-item-fr">{{list.time}}</span>
				</a>
			</div>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				lists: [
					{
						"tit1": "行业通知",
						"tit2": "推荐全省交通运输行业精神文明建设先进集体先进个人公示",
						"time": "2020-04-26 08:48",
						"img": '../../static/icon-item-001.png'
					},
					{
						"tit1": "我的待办",
						"tit2": "沪陕高速公路沿线（京沪2016-00136号）设置广告设施许可申请",
						"time": "2020-04-25 15:05",
						"img": '../../static/icon-item-002.png'
					},
					// {
					// 	"tit1": "账户通知",
					// 	"tit2": "恭喜你参加的拼团已组成成功了，请您等待卖家发货",
					// 	"time": "昨天",
					// 	"img": '../../static/icon-item-003.png'
					// },
					{
						"tit1": "互动问答",
						"tit2": "在高速公路用地范围内架设、埋设管道、电缆等设施",
						"time": "2020-04-26 11:38",
						"img": '../../static/icon-item-004.png'
					},
					{
						"tit1": "物流助手",
						"tit2": "您的许可申请书已发货，请您等待收货",
						"time": "2020-04-26 09:47",
						"img": '../../static/icon-item-005.png'
					},
				],
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	@import '../../css/style.css';
</style>
