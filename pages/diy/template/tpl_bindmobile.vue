<template>
<view class="fui-cell-group fui-cell-click" v-if="member.needbind==1" style="margin-top:0">
    <navigator class="fui-cell" hover-class="none" url="/pages/member/bind/index" open-type="navigate">
        <view class="fui-cell-icon">
            <text class="icox icox-mobilephone"></text>
        </view>
        <view class="fui-cell-text"><p class="text text-danger">{{ diyitem.params.title }}</p></view>
        <view class="fui-cell-remark"></view>
    </navigator>
    <view class="fui-cell-tip">{{ diyitem.params.text }}</view>
</view>
</template>


	<script> 
		
		export default {
			props: []
		}
	</script> 
									