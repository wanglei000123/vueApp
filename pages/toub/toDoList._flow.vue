<template>
	<view>
		<view class="cu-form-group">
			<view class="title">是否同意</view>
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
		
		<view class="cu-form-group">
			<view class="title">审批意见</view>
			<textarea maxlength="-1" :disabled="modalName!=null" @input="textareaAInput" placeholder="请输入审批意见"></textarea>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
				return {
					
				};
			},
			methods: {
				
			}
		}
</script>

<style>
	
</style>
