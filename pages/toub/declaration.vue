<template>
	<view>
		<cu-custom bgColor="bg-gradual-blue" :isBack="true">
			<block slot="backText">返回</block>
			<block slot="content">网上申报</block>
		</cu-custom>
		<form>
			<!-- <view class="cu-bar bg-white">
				<view class="action">
					<text class="cuIcon-titles text-green"></text>
					<text class="text-xl text-bold">事项信息</text>
				</view>
			</view> -->
			
			<view class="cu-form-group margin-top">
				<view class="title">办件名称</view>
				<input placeholder="办件名称" name="input"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">事项地点</view>
				<input placeholder="事项地点" name="input"></input>
				<text class='cuIcon-locationfill text-orange'></text>
			</view>
			<view class="cu-form-group">
				<view class="title">所在路线</view>
				<input placeholder="如G42" name="input"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">路线桩号</view>
				<input placeholder="如765.2~853.6" name="input"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">申请类型</view>
				<picker @change="shenqlxChange" :value="shenqlxIndex" :range="shenqlx">
					<view class="picker">
						{{shenqlxIndex>-1?shenqlx[shenqlxIndex]:'选择申请类型'}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">申请原案号</view>
				<input placeholder="延续、变更申请原案号" name="input"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">指定许可单位</view>
				<input placeholder="指定许可单位" name="input"></input>
			</view>
			
			<view class="cu-form-group margin-top">
				<view class="title">申请者类别</view>
				<picker @change="shenqzlbChange" :value="shenqzlbIndex" :range="shenqzlb">
					<view class="picker">
						{{shenqzlbIndex>-1?shenqzlb[shenqzlbIndex]:'选择申请者类别'}}
					</view>
				</picker>
			</view>
			<view v-if="zrr" class="cu-form-group">
				<view class="title">姓名</view>
				<input placeholder="姓名" name="input"></input>
			</view>
			<view v-if="zrr" class="cu-form-group">
				<view class="title">证件类型</view>
				<picker @change="zhengjlxChange" :value="zhengjlxIndex" :range="zhengjlx">
					<view class="picker">
						{{zhengjlxIndex>-1?zhengjlx[zhengjlxIndex]:'选择证件类型'}}
					</view>
				</picker>
			</view>
			<view v-if="zrr" class="cu-form-group">
				<view class="title">证件号码</view>
				<input placeholder="证件号码" name="input"></input>
			</view>
			<view v-if="zrr" class="cu-form-group">
				<view class="title">电话</view>
				<input placeholder="收件人电话" name="input"></input>
				<view class="cu-capsule radius">
					<view class='cu-tag bg-blue '>
						+86
					</view>
					<view class="cu-tag line-blue">
						中国大陆
					</view>
				</view>
			</view>
			<view v-if="fr" class="cu-form-group">
				<view class="title">单位名称</view>
				<input placeholder="单位名称" name="input"></input>
			</view>
			<view v-if="fr" class="cu-form-group">
				<view class="title">证件类型</view>
				<picker @change="frzhengjlxChange" :value="frzhengjlxIndex" :range="frzhengjlx">
					<view class="picker">
						{{frzhengjlxIndex>-1?frzhengjlx[frzhengjlxIndex]:'选择证件类型'}}
					</view>
				</picker>
			</view>
			<view v-if="fr" class="cu-form-group">
				<view class="title">证件号码</view>
				<input placeholder="证件号码" name="input"></input>
			</view>
			<view v-if="fr" class="cu-form-group">
				<view class="title">法人/负责人</view>
				<input placeholder="法人/负责人" name="input"></input>
			</view>
			
			<view class="cu-form-group margin-top">
				<view class="title">收件人名称</view>
				<input placeholder="收件人名称" name="input"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">收件人电话</view>
				<input placeholder="收件人电话" name="input"></input>
				<view class="cu-capsule radius">
					<view class='cu-tag bg-blue '>
						+86
					</view>
					<view class="cu-tag line-blue">
						中国大陆
					</view>
				</view>
			</view>
			<view class="cu-form-group">
				<view class="title">收件省/市/县</view>
				<picker mode="multiSelector" @change="MultiChange" @columnchange="MultiColumnChange" :value="multiIndex" :range="multiArray">
					<view class="picker">
						{{multiArray[0][multiIndex[0]]}}，{{multiArray[1][multiIndex[1]]}}，{{multiArray[2][multiIndex[2]]}}
					</view>
				</picker>
			</view>
			<view class="cu-form-group">
				<view class="title">收件地址</view>
				<input placeholder="收件地址" name="input"></input>
				<text class='cuIcon-locationfill text-orange'></text>
			</view>
			
			<view class="cu-form-group margin-top">
				<view class="title">办理摘要</view>
				<input placeholder="办理摘要" name="input"></input>
			</view>
			<view class="cu-bar bg-white">
				<view class="action">
					附件上传
				</view>
				<view class="action">
					{{imgList.length}}/12
				</view>
			</view>
			<view class="cu-form-group">
				<view class="grid col-4 grid-square flex-sub">
					<view class="bg-img" v-for="(item,index) in imgList" :key="index" @tap="ViewImage" :data-url="imgList[index]">
					 <image :src="imgList[index]" mode="aspectFill"></image>
						<view class="cu-tag bg-red" @tap.stop="DelImg" :data-index="index">
							<text class='cuIcon-close'></text>
						</view>
					</view>
					<view class="solids" @tap="ChooseImage" v-if="imgList.length<12">
						<text class='cuIcon-cameraadd'></text>
					</view>
				</view>
			</view>
			
			<!-- <view class="cu-form-group margin-top">
				<view class="title">承诺书上传</view>
				<upload></upload> 
			</view> -->
			<view class="cu-bar bg-white">
				<view class="action">
					承诺书上传
				</view>
				<view class="action">
					{{imgCnsList.length}}/4
				</view>
			</view>
			<view class="cu-form-group">
				<view class="grid col-4 grid-square flex-sub">
					<view class="bg-img" v-for="(item,index) in imgCnsList" :key="index" @tap="ViewCnsImage" :data-url="imgCnsList[index]">
					 <image :src="imgCnsList[index]" mode="aspectFill"></image>
						<view class="cu-tag bg-red" @tap.stop="DelCnsImg" :data-index="index">
							<text class='cuIcon-close'></text>
						</view>
					</view>
					<view class="solids" @tap="ChooseCnsImage" v-if="imgCnsList.length<4">
						<text class='cuIcon-cameraadd'></text>
					</view>
				</view>
			</view>
			
			<view class="issue-btn-box margin-top" style="margin-bottom: 10px;">
				<button class="submit-btn" type="primary" style="width: 80%;">提交</button>
				<slot name="submit"></slot>
			</view>
		</form>
	</view>
</template>

<script>
	import upload from "@/pages/toub/declaration_fileUpload.vue";
	export default {
		components: {
			upload
		},
		data() {
			return {
				shenqlxIndex: -1,
				shenqlx: ['一般申请', '延续申请', '变更申请'],
				zrr: true,
				fr: false,
				shenqzlbIndex: 0,
				shenqzlb: ['自然人', '法人'],
				zhengjlxIndex: 0,
				zhengjlx: ['身份证', '护照', '居住证', '台胞证', '通行证'],
				frzhengjlxIndex: 0,
				frzhengjlx: ['身份证', '护照', '居住证', '台胞证', '通行证'],
				index: -1,
				picker: ['喵喵喵', '汪汪汪', '哼唧哼唧'],
				multiArray: [
					['江苏省'],
					['南京市', '无锡市', '徐州市', '常州市', '苏州市', '南通市',
					 '淮安市', '连云港市', '盐城市', '扬州市', '镇江市', '泰州市', '宿迁市'],
					['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区']
				],
				objectMultiArray: [
					[{
							id: 0,
							name: '无脊柱动物'
						},
						{
							id: 1,
							name: '脊柱动物'
						}
					],
					[{
							id: 0,
							name: '扁性动物'
						},
						{
							id: 1,
							name: '线形动物'
						},
						{
							id: 2,
							name: '环节动物'
						},
						{
							id: 3,
							name: '软体动物'
						},
						{
							id: 3,
							name: '节肢动物'
						}
					],
					[{
							id: 0,
							name: '猪肉绦虫'
						},
						{
							id: 1,
							name: '吸血虫'
						}
					]
				],
				multiIndex: [0, 0, 0],
				time: '12:01',
				date: '2018-12-25',
				region: ['江苏省', '南京市', '鼓楼区'],
				switchA: false,
				switchB: true,
				switchC: false,
				switchD: false,
				radio: 'A',
				checkbox: [{
					value: 'A',
					checked: true
				}, {
					value: 'B',
					checked: true
				}, {
					value: 'C',
					checked: false
				}],
				imgList: [],
				modalName: null,
				textareaAValue: '',
				textareaBValue: '',
				imgCnsList: [],
			};
		},
		methods: {
			shenqlxChange(e) {
				this.shenqlxIndex = e.detail.value
			},
			shenqzlbChange(e) {
				this.shenqzlbIndex = e.detail.value;
				if(this.shenqzlbIndex === 0){
					this.fr = false;
					this.zrr = true;
				} else {
					this.fr = true;
					this.zrr = false;
				}
			},
			zhengjlxChange(e) {
				this.zhengjlxIndex = e.detail.value
			},
			frzhengjlxChange(e) {
				this.frzhengjlxIndex = e.detail.value
			},
			PickerChange(e) {
				this.index = e.detail.value
			},
			MultiChange(e) {
				this.multiIndex = e.detail.value
			},
			MultiColumnChange(e) {
				let data = {
					multiArray: this.multiArray,
					multiIndex: this.multiIndex
				};
				data.multiIndex[e.detail.column] = e.detail.value;
				switch (e.detail.column) {
					case 0:
						switch (data.multiIndex[0]) {
							case 0:
								data.multiArray[1] = ['扁性动物', '线形动物', '环节动物', '软体动物', '节肢动物'];
								data.multiArray[2] = ['猪肉绦虫', '吸血虫'];
								break;
							case 1:
								data.multiArray[1] = ['鱼', '两栖动物', '爬行动物'];
								data.multiArray[2] = ['鲫鱼', '带鱼'];
								break;
						}
						data.multiIndex[1] = 0;
						data.multiIndex[2] = 0;
						break;
					case 1:
						switch (data.multiIndex[0]) {
							case 0:
								switch (data.multiIndex[1]) {
									case 0:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
									case 1:
										data.multiArray[2] = ['崇安区', '南长区', '北塘区', '锡山区', '惠山区', '滨湖区', '江阴市', '宜兴市'];
										break;
									case 2:
										data.multiArray[2] = ['鼓楼区', '云龙区', '贾汪区', '泉山区', '铜山区', '丰县', '沛县', '睢宁县', '新沂市', '邳州市'];
										break;
									case 3:
										data.multiArray[2] = ['虎丘区', '吴中区', '相城区', '姑苏区', '吴江区', '常熟市', '张家港市', '昆山市', '太仓市'];
										break;
									case 4:
										data.multiArray[2] = ['崇川区', '港闸区', '通州区', '海安县', '如东县', '启东市', '如皋市', '海门市'];
										break;
									case 5:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
									case 6:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
									case 7:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
									case 8:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
									case 9:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
									case 10:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
									case 11:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
									case 12:
										data.multiArray[2] = ['鼓楼区', '建邺区', '玄武区', '秦淮区', '浦口区', '栖霞区', '雨花台区', '六合区', '溧水区', '高淳区'];
										break;
								}
								break;
							case 1:
								switch (data.multiIndex[1]) {
									case 0:
										data.multiArray[2] = ['鲫鱼', '带鱼'];
										break;
									case 1:
										data.multiArray[2] = ['青蛙', '娃娃鱼'];
										break;
									case 2:
										data.multiArray[2] = ['蜥蜴', '龟', '壁虎'];
										break;
								}
								break;
						}
						data.multiIndex[2] = 0;
						break;
				}
				this.multiArray = data.multiArray;
				this.multiIndex = data.multiIndex;
			},
			TimeChange(e) {
				this.time = e.detail.value
			},
			DateChange(e) {
				this.date = e.detail.value
			},
			RegionChange(e) {
				this.region = e.detail.value
			},
			SwitchA(e) {
				this.switchA = e.detail.value
			},
			SwitchB(e) {
				this.switchB = e.detail.value
			},
			SwitchC(e) {
				this.switchC = e.detail.value
			},
			SwitchD(e) {
				this.switchD = e.detail.value
			},
			RadioChange(e) {
				this.radio = e.detail.value
			},
			CheckboxChange(e) {
				var items = this.checkbox,
					values = e.detail.value;
				for (var i = 0, lenI = items.length; i < lenI; ++i) {
					items[i].checked = false;
					for (var j = 0, lenJ = values.length; j < lenJ; ++j) {
						if (items[i].value == values[j]) {
							items[i].checked = true;
							break
						}
					}
				}
			},
			ChooseImage() {
				uni.chooseImage({
					count: 12, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: (res) => {
						if (this.imgList.length != 0) {
							this.imgList = this.imgList.concat(res.tempFilePaths)
						} else {
							this.imgList = res.tempFilePaths
						}
					}
				});
			},
			ViewImage(e) {
				uni.previewImage({
					urls: this.imgList,
					current: e.currentTarget.dataset.url
				});
			},
			DelImg(e) {
				uni.showModal({
					title: '一体化政务平台',
					content: '确定要删除吗？',
					cancelText: '再看看',
					confirmText: '再见',
					success: res => {
						if (res.confirm) {
							this.imgList.splice(e.currentTarget.dataset.index, 1)
						}
					}
				})
			},
			textareaAInput(e) {
				this.textareaAValue = e.detail.value
			},
			textareaBInput(e) {
				this.textareaBValue = e.detail.value
			},
			ChooseCnsImage() {
				uni.chooseImage({
					count: 4, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: (res) => {
						if (this.imgCnsList.length != 0) {
							this.imgCnsList = this.imgCnsList.concat(res.tempFilePaths)
						} else {
							this.imgCnsList = res.tempFilePaths
						}
					}
				});
			},
			ViewCnsImage(e) {
				uni.previewImage({
					urls: this.imgCnsList,
					current: e.currentTarget.dataset.url
				});
			},
			DelCnsImg(e) {
				uni.showModal({
					title: '一体化政务平台',
					content: '确定要删除吗？',
					cancelText: '再看看',
					confirmText: '再见',
					success: res => {
						if (res.confirm) {
							this.imgCnsList.splice(e.currentTarget.dataset.index, 1)
						}
					}
				})
			},
		}
	}
</script>

<style>
	.cu-form-group .title {
		min-width: calc(4em + 15px);
	}
</style>
