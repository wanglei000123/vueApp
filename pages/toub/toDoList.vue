<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">我的办件</block>
		</cu-custom>
		
		<!-- <view class="cu-bar search bg-white">
			<view class="search-form round">
				<text class="cuIcon-search"></text>
				<input @focus="InputFocus" @blur="InputBlur" :adjust-position="false" type="text" placeholder="输入事项、案号关键词" confirm-type="search"></input>
			</view>
			<view class="action">
				<button class="cu-btn bg-green shadow-blur round">搜索</button>
			</view>
			<view class="action">
				<button class="cu-btn bg-green shadow" @tap="showModal" data-target="menuModal">设置</button>
			</view>
		</view> -->
		
		<view class="cu-modal" :class="modalName=='menuModal'?'show':''" @tap="hideModal">
			<view class="cu-dialog" @tap.stop>
				<view class="cu-list menu text-left solid-top">
					<view class="cu-item">
						<view class="content">
							<text class="text-grey">短边框</text>
						</view>
						<view class="action">
							<switch @change="MenuBorder" :class="menuBorder?'checked':''" :checked="menuBorder?true:false"></switch>
						</view>
					</view>
					<view class="cu-item">
						<view class="content">
							<text class="text-grey">箭头</text>
						</view>
						<view class="action">
							<switch @change="MenuArrow" :class="menuArrow?'checked':''" :checked="menuArrow?true:false"></switch>
						</view>
					</view>
					<view class="cu-item">
						<view class="content">
							<text class="text-grey">卡片</text>
						</view>
						<view class="action">
							<switch @change="MenuCard" :class="menuCard?'checked':''" :checked="menuCard?true:false"></switch>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="cu-list menu" :class="[menuBorder?'sm-border':'',menuCard?'card-menu margin-top':'']" @tap="showStepModal" data-target="DialogStepModal">
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">事项名称：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-formfill text-orange"></text>
					<text class="text-grey">上河楚州千伏线路跨越盐洛高速</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">事项案号：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-circlefill text-blue"></text>
					<text class="text-grey">苏高许字[2020]00143号</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">业务类别：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-infofill text-red"></text>
					<text class="text-grey">公路管理</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">受理时间：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-timefill text-green"></text>
					<text class="text-grey">2020-04-16 14:34</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">受理状态：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-radioboxfill text-purple"></text>
					<text class="text-grey">技术审查</text>
				</view>
			</view>
		</view>
		
		<view class="cu-list menu" :class="[menuBorder?'sm-border':'',menuCard?'card-menu margin-top':'']" @tap="showStepModal" data-target="DialogStepModal">
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">事项名称：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-formfill text-orange"></text>
					<text class="text-grey">S268跨京沪高速公路大桥</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">事项案号：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-circlefill text-blue"></text>
					<text class="text-grey">苏高许字[2020]00124号</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">业务类别：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-infofill text-red"></text>
					<text class="text-grey">公路管理</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">受理时间：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-timefill text-green"></text>
					<text class="text-grey">2020-04-16 14:10</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">受理状态：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-radioboxfill text-purple"></text>
					<text class="text-grey">审核</text>
				</view>
			</view>
		</view>
		
		<view class="cu-list menu" :class="[menuBorder?'sm-border':'',menuCard?'card-menu margin-top':'']" @tap="showStepModal" data-target="DialogStepModal">
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">事项名称：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-formfill text-orange"></text>
					<text class="text-grey">沪陕高速设置广告设施许可申请</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">事项案号：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-circlefill text-blue"></text>
					<text class="text-grey">苏高许字[2020]00136号</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">业务类别：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-infofill text-red"></text>
					<text class="text-grey">公路管理</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">受理时间：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-timefill text-green"></text>
					<text class="text-grey">2020-04-16 14:09</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">受理状态：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-radioboxfill text-purple"></text>
					<text class="text-grey">审批</text>
				</view>
			</view>
		</view>
		
		<view class="cu-list menu" :class="[menuBorder?'sm-border':'',menuCard?'card-menu margin-top':'']" @tap="showStepModal" data-target="DialogStepModal">
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">事项名称：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-formfill text-orange"></text>
					<text class="text-grey">沪宁高速公路大中修养护工程</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">事项案号：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-circlefill text-blue"></text>
					<text class="text-grey">苏高许字[2020]00129号</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">业务类别：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-infofill text-red"></text>
					<text class="text-grey">公路管理</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">受理时间：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-timefill text-green"></text>
					<text class="text-grey">2020-04-16 10:04</text>
				</view>
			</view>
			<view class="cu-item" :class="menuArrow?'arrow':''">
				<view class="title">受理状态：</view>
				<view class="content" style="margin-left: 1vw;">
					<text class="cuIcon-radioboxfill text-purple"></text>
					<text class="text-grey">文书送达</text>
				</view>
			</view>
		</view>
		
		<view class="cu-modal" :class="setpModalName=='DialogStepModal'?'show':''">
			<view class="cu-dialog">
				<view class="cu-bar bg-white justify-end">
					<view class="content">审批意见</view>
					<view class="action" @tap="hideStepModal">
						<text class="cuIcon-close text-red"></text>
					</view>
				</view>
				<view class="padding-xl">
					<flow></flow>
				</view>
				<view class="cu-bar bg-white justify-end">
					<view class="action">
						<button class="cu-btn line-green text-green" @tap="hideStepModal">取消</button>
						<button class="cu-btn bg-green margin-left" @tap="hideStepModal">确定</button>
		
					</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	import flow from './toDoList._flow.vue';
	export default {
		components: {
			flow
		},
		data() {
				return {
					cuIconList: [{
						cuIcon: 'cardboardfill',
						color: 'red',
						badge: 120,
						name: 'VR'
					}, {
						cuIcon: 'recordfill',
						color: 'orange',
						badge: 1,
						name: '录像'
					}, {
						cuIcon: 'picfill',
						color: 'yellow',
						badge: 0,
						name: '图像'
					}, {
						cuIcon: 'noticefill',
						color: 'olive',
						badge: 22,
						name: '通知'
					}, {
						cuIcon: 'upstagefill',
						color: 'cyan',
						badge: 0,
						name: '排行榜'
					}, {
						cuIcon: 'clothesfill',
						color: 'blue',
						badge: 0,
						name: '皮肤'
					}, {
						cuIcon: 'discoverfill',
						color: 'purple',
						badge: 0,
						name: '发现'
					}, {
						cuIcon: 'questionfill',
						color: 'mauve',
						badge: 0,
						name: '帮助'
					}, {
						cuIcon: 'commandfill',
						color: 'purple',
						badge: 0,
						name: '问答'
					}, {
						cuIcon: 'brandfill',
						color: 'mauve',
						badge: 0,
						name: '版权'
					}],
					modalName: null,
					gridCol: 3,
					gridBorder: false,
					menuBorder: false,
					menuArrow: false,
					menuCard: true,
					skin: false,
					listTouchStart: 0,
					listTouchDirection: null,
					setpModalName: null,
				};
			},
			methods: {
				showModal(e) {
					this.modalName = e.currentTarget.dataset.target
				},
				hideModal(e) {
					this.modalName = null
				},
				Gridchange(e) {
					this.gridCol = e.detail.value
				},
				Gridswitch(e) {
					this.gridBorder = e.detail.value
				},
				MenuBorder(e) {
					this.menuBorder = e.detail.value
				},
				MenuArrow(e) {
					this.menuArrow = e.detail.value
				},
				MenuCard(e) {
					this.menuCard = e.detail.value
				},
				SwitchSex(e) {
					this.skin = e.detail.value
				},
		
				// ListTouch触摸开始
				ListTouchStart(e) {
					this.listTouchStart = e.touches[0].pageX
				},
		
				// ListTouch计算方向
				ListTouchMove(e) {
					this.listTouchDirection = e.touches[0].pageX - this.listTouchStart > 0 ? 'right' : 'left'
				},
		
				// ListTouch计算滚动
				ListTouchEnd(e) {
					if (this.listTouchDirection == 'left') {
						this.modalName = e.currentTarget.dataset.target
					} else {
						this.modalName = null
					}
					this.listTouchDirection = null
				},
				
				showStepModal(e) {
					this.setpModalName = e.currentTarget.dataset.target
				},
				hideStepModal(e) {
					this.setpModalName = null
				},
			}
		}
</script>

<style>
	.page {
		height: 100Vh;
		width: 100vw;
	}
	
	.page.show {
		overflow: hidden;
	}
	
	.switch-sex::after {
		content: "\e716";
	}
	
	.switch-sex::before {
		content: "\e7a9";
	}
	
	.switch-music::after {
		content: "\e66a";
	}
	
	.switch-music::before {
		content: "\e6db";
	}
	
	.padding-xl {
		padding: 8px;
	}
</style>
