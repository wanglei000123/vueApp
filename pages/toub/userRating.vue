<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">用户评价</block>
		</cu-custom>
		
		<scroll-view scroll-x class="bg-white nav">
			<view class="flex text-center">
				<view class="cu-item flex-sub" :class="index==TabCur?'text-blue cur':''" v-for="(item,index) in tabList" :key="index" @tap="tabSelect" :data-id="index">
					{{item}}
				</view>
			</view>
		</scroll-view>
		
		<block v-if="TabCur==0">
			<view class="cu-form-group margin-top">
				<view class="title">服务态度</view>
				<picker @change="fuwtdChange" :value="fuwtdIndex" :range="fuwtd">
					<view class="picker">
						{{fuwtdIndex>-1?fuwtd[fuwtdIndex]:'选择服务态度'}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">服务水平</view>
					<picker @change="fuwspChange" :value="fuwspIndex" :range="fuwsp">
						<view class="picker">
							{{fuwspIndex>-1?fuwsp[fuwspIndex]:'选择服务水平'}}
						</view>
					</picker>
				</view>
				
				<view class="issue-btn-box margin-top">
					<button class="submit-btn" type="primary" >提交</button>
					<slot name="submit"></slot>
				</view>
		</block>
		<block v-if="TabCur==1">
			<view class="cu-form-group margin-top">
				<view class="title">投诉部门</view>
				<picker @change="tousbmChange" :value="tousbmIndex" :range="tousbm">
					<view class="picker">
						{{tousbmIndex>-1?tousbm[tousbmIndex]:'选择投诉部门'}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">事项类别</view>
				<picker @change="shixlbChange" :value="shixlbIndex" :range="shixlb">
					<view class="picker">
						{{shixlbIndex>-1?shixlb[shixlbIndex]:'选择事项类别'}}
					</view>
				</picker>
			</view>
			
			<view class="cu-form-group">
				<view class="title">是否公开</view>
					<radio-group @change="SetBorderSize">
						<label class="margin-left-sm">
							<radio class="blue radio" value="" checked></radio>
							<text class="margin-left-sm">是</text>
						</label>
						<label class="margin-left-sm">
							<radio class="blue radio" value="s"></radio>
							<text class="margin-left-sm">否</text>
						</label>
					</radio-group>
				</view>
				
				<view class="cu-form-group margin-top">
					<textarea maxlength="-1" :disabled="modalName!=null" @input="textareaAInput" placeholder="请输入投诉述求"></textarea>
				</view>
				
				<view class="issue-btn-box margin-top">
					<button class="submit-btn" type="primary" >提交</button>
					<slot name="submit"></slot>
				</view>
		</block>
		<block v-if="TabCur==2">
			<view class="cu-form-group margin-top">
				<textarea maxlength="-1" :disabled="modalName!=null" @input="textareaAInput" placeholder="请对我们的软件进行评价，填写你的意见"></textarea>
			</view>
			
			<view class="issue-btn-box margin-top">
				<button class="submit-btn" type="primary" >提交</button>
				<slot name="submit"></slot>
			</view>
		</block>
		
		<!-- <view class="content">
			<my-issue key="1" :score="3"/>
			<my-issue key="2" :score="3" />
			<my-issue key="3" :starsDisabled="true" />
		</view> -->
		
	</view>
</template>

<script>
  import myIssue from '@/pages/toub/userRating_com.vue'
	export default {
		components:{myIssue},
		data() {
			return {
				TabCur: 0,
				tabList: ['满意度评价', '用户投诉', '用户建议'],
				title: 'Hello',
				fuwtdIndex: -1,
				fuwtd: ['非常满意', '满意', '基本满意', '不满意', '非常不满意'],
				fuwspIndex: -1,
				fuwsp: ['非常满意', '满意', '基本满意', '不满意', '非常不满意'],
				tousbmIndex: -1,
				tousbm: ['交通运输厅', '港航中心', '公路中心', '综合执法局'],
				shixlbIndex: -1,
				shixlb: ['收费公路的鉴定和验收', '公路施工作业验收', '集装箱装箱现场检查员资格认可', '变更企业办公地点备案', '变更企业法定代表人备案'],
			}
		},
		onLoad() {

		},
		methods: {
			tabSelect(e) {
				this.TabCur = e.currentTarget.dataset.id;
			},
			fuwspChange(e) {
				this.fuwspIndex = e.detail.value
			},
			fuwtdChange(e) {
				this.fuwtdIndex = e.detail.value
			},
			tousbmChange(e) {
				this.tousbmIndex = e.detail.value
			},
			shixlbChange(e) {
				this.shixlbIndex = e.detail.value
			},
		}
	}
</script>

<style>
	.content{
		height: 100%;
	}
</style>
