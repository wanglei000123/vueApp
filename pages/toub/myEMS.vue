<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">我的EMS</block>
		</cu-custom>
		<view class="content">
			<div class="aui-news-box">
				<navigator url="/pages/toub/myEMS_lc" class="aui-news-item" v-for="(list, i) in lists" :key="i">
					<div class="aui-news-item-hd">
						<img :src="list.img" alt="">
					</div>
					<div class="aui-news-item-bd">
						<h4>{{list.tit1}}</h4>
						<p>{{list.tit2}}</p>
					</div>
					<span class="aui-news-item-fr">{{list.time}}</span>
				</navigator>
			</div>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				dataUrl: 'index',
				lists: [
					{
						"tit1": "待收货",
						"tit2": "申通快递：773033252409864",
						"time": "",
						"img": '../../static/sto.png'
					},
					{
						"tit1": "待收货",
						"tit2": "顺丰快递：SF3302946445813",
						"time": "",
						"img": '../../static/sf.png'
					},
					{
						"tit1": "待收货",
						"tit2": "圆通快递：YT4454946445813",
						"time": "",
						"img": '../../static/yt.png'
					},
					{
						"tit1": "已签收",
						"tit2": "百世快递：557003879467729",
						"time": "",
						"img": '../../static/bs.png'
					},
				],
				alidata2: {
					state: 3,
					uptime: '2020-04-24 10:58:24',
					data: [
						{
							time: '2020-04-20 16:27:31',
							remark: '南京市【南京鼓楼区十八部】，公司门口！详情致电17609715305 已签收'
						},
						{
							time: '2020-04-20 14:03:11',
							remark: '南京市【南京鼓楼区十八部】，【谭德银17609715305】正在派件'
						},
						{
							time: '2020-04-20 10:53:15',
							remark: '到南京市【南京鼓楼区十八部】'
						},
						{
							time: '2020-04-20 04:22:38',
							remark: '南京市【南京转运营业中心】，正发往【南京鼓楼区十八部】'
						},
						{
							time: '2020-04-20 03:30:17',
							remark: '到南京市【南京转运中心】'
						},
						{
							time: '2020-04-19 21:46:27',
							remark: '苏州市【无锡转运中心】，正发往【南京转运中心】'
						},
						{
							time: '2020-04-19 21:43:28',
							remark: '到苏州市【无锡转运中心】'
						},
						{
							time: '2020-04-19 17:11:40',
							remark: '到南通市【海门】'
						},
						{
							time: '2020-04-19 13:17:56',
							remark: '南通市【海门】，【金喜露18068137656】已揽收'
						}
					],
					information: {
						no: '70939995911523',
						sName: 'HTKY',
						expName: '百世快递(原汇通)',
						url: 'http:www.htky365.com',
						tel: '021-62963636',
						img: 'https:oss-cn2.apistore.cnexpHTKY.png'
					}
				}
			}
		},
		onLoad() {

		},
		methods: {
			kuaidxq(e){
				this.$router.push('./myEMS_lc');
			},
		}
	}
</script>

<style>
	@import '../../css/style.css';
</style>
