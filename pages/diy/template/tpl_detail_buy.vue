<template>
<block v-if="goods.canbuy">
    <view :class="'fui-navbar bottom-buttons ' + iphonexnavbar">
        <view v-if="!limits" class="nav-item favorite-item" @tap="favorite">
            <view :class="'icox ' + ( goods.isfavorite?'icox-likefill':'icox-like')"></view>
            <view class="label">关注</view>
        </view>
        <view :class="'nav-item favorite-item ' + ( goods.isfavorite?'active':'')" @tap="favorite" :data-isfavorite="( goods.isfavorite?1:0 )" v-if="goods.customer!=1 && limits">
            <view :class="'icox ' + ( goods.isfavorite?'icox-likefill':'icox-like')"></view>
            <view class="label">关注</view>
        </view>
        <button class="nav-item customer-item" open-type="contact" v-if="goods.customer==1 && limits" session-from="weapp" show-message-card="true">
            <view class="icox icox-customerservice"></view>
            <view class="label">客服</view>
        </button> 
        <navigator class="nav-item external" :url="'/pages/index/index?merchid=' + goods.merchid" open-type="switchTab">
            <view class="icox icox-shop1"></view>
            <view class="label">店铺</view>
        </navigator>
        <view class="nav-item cart-item" id="menucart" @tap="menucart">
            <block v-if="goods.cartcount && limits">
                <view :class="'badge ' + (goods.cartount<=0?'out':'in')">{{goods.cartcount}}</view>
            </block>
            <view class="icox icox-cart1"></view>
            <view class="label">购物车</view>
        </view>
        <view v-if="goods.canAddCart" class="nav-item btn cartbtn" @tap="selectPicker" :data-tap="active" :data-id="goods.id" data-buytype="cart">加入购物车</view>
        <view class="nav-item btn buybtn" @tap="selectPicker" :data-tap="active" data-buytype="buy" :data-id="goods.id">立刻购买</view>
    </view>
</block>
</template>


	<script> 
		
		export default {
			props: []
		}
	</script> 
									