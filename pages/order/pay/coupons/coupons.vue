<template>
<view class="page">
  <view class="coupon-headblock">
    <view class="top-layer"></view>
    <view class="line-layer"></view>
    <view class="bottom-layer"></view>
    <view class="gold" :style="'background-image: url('' + approot + 'template/mobile/default/static/images/gold.png')'"></view>
    <view class="link-text">请至【
      <navigator class="inline" hover-class="none" url="/pages/sale/coupon/my/index/index" open-type="redirect">我的优惠券</navigator>】查看</view>
    <view class="paper">
      <view class="title">恭喜获得</view>
      <view class="text">
        <i class="d1"></i>
        <i class="d2"></i>
        <p class="t1">1张优惠券</p>
      </view>
      <i class="line"></i>
      <i class="dot-top"></i>
      <i class="dot-left"></i>
      <i class="dot-right"></i>
      <i class="dot-1"></i>
      <i class="dot-2"></i>
      <i class="dot-3"></i>
      <i class="dot-4"></i>
      <i class="dot-5"></i>
      <i class="dot-6"></i>
    </view>
  </view>

<view id="container" class="coupon-container coupon-index-list">

	<view href class="coupon-index-list-a  blue">
		<view class="fui-list coupon-list">
			<span class="coupon-ling"><image src="https://jqnyrv.ifkvip.com/addons/ewei_shopv2/template/mobile/default/static/images/coupon/ling.png" alt></image></span>
			<view class="fui-list-inner coupon-index-list-left">
				<b style="width: 92px ; text-align:center ;">满减券</b>
				<view class="coupon-index-list-info fui-list">
					<view class="fui-list-media">
						<image src=" https://jqnyrv.ifkvip.com/attachment/images/4/2017/12/k9z004aLNRNROWWiUNWNloIWU7l90l.png" alt></image>
					</view>
					<view class="fui-list-inner">
						<view class="h3">新人50元券</view>
						<view class="coupon-full"> 消费满150元立减50元</view>
						<view class="coupon-time">有效期 2018-01-24 </view>
					</view>
				</view>
			</view>
			<view class="fui-list-media coupon-index-list-right">
				<view class="forth0 circle coupon-list-canvas"></view>
				<i class="coupon-list-ling">立即使用</i>
			</view>
		</view>
	</view>
</view>

  <navigator class="btn btn-danger block" hover-class="none" url="/pages/sale/coupon/index/index" open-type="redirect" style="margin: 0 20rpx 20rpx;">继续领取优惠券</navigator>

  <navigator class="btn btn-default block" hover-class="none" url="/pages/sale/coupon/my/index/index" open-type="redirect" style="margin: 0 20rpx 20rpx;">查看我的优惠券</navigator>
</view>
</template>

<script>

export default {
  data() {
    return {};
  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {},

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {},

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {},

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {},

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {},

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {},

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {},

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {},
  components: {},
  props: {},
  methods: {
    setData: function (obj) {
      let that = this;
      let keys = [];
      let val, data;
      Object.keys(obj).forEach(function (key) {
        keys = key.split('.');
        val = obj[key];
        data = that.$data;
        keys.forEach(function (key2, index) {
          if (index + 1 == keys.length) {
            that.$set(data, key2, val);
          } else {
            if (!data[key2]) {
              that.$set(data, key2, {});
            }
          }

          data = data[key2];
        });
      });
    }
  }
};
</script>
<style>
.coupon-headblock {
    position: relative;
    height: 480rpx;
    background: #fe5d5c;
    overflow: hidden;
}
.coupon-headblock .line-layer {
    width: 0;
    height: 110rpx;
    border-left: 800rpx solid #ffcf6f;
    border-right: 800rpx solid #ffcf6f;
    border-top: 100rpx solid transparent;
    position: absolute;
    left: 50%;
    margin-left: -800rpx;
    bottom: 0;
    z-index: 3;
}
.coupon-headblock .bottom-layer {
    width: 0;
    height: 110rpx;
    border-left: 800rpx solid #fe5d5c;
    border-right: 800rpx solid #fe5d5c;
    border-top: 100rpx solid transparent;
    position: absolute;
    left: 50%;
    margin-left: -800rpx;
    bottom: -10rpx;
    z-index: 4;
}
.coupon-headblock .top-layer {
    width: 0;
    height: 200rpx;
    border-left: 800rpx solid #f74a4a;
    border-right: 800rpx solid #f74a4a;
    border-bottom: 100rpx solid transparent;
    position: absolute;
    left: 50%;
    margin-left: -800rpx;
    top: 0;
    z-index: 1;
}
.coupon-headblock .gold {
    height: 100rpx;
    width: 100rpx;
    background-repeat: no-repeat;
    background-size: 100%;
    background-position: center;
    position: absolute;
    left: 50%;
    margin-left: -48rpx;
    bottom: 50rpx;
    z-index: 5;
}
.coupon-headblock .paper {
    height:320rpx;
    width:360rpx;
    background: #fff;
    position: absolute;
    top:80rpx;
    left: 50%;
    margin-left: -180rpx;
    z-index: 2;
}
.coupon-headblock .paper .line {
    height: 0;
    position: absolute;
    top:120rpx;
    left: 20rpx;
    right: 20rpx;
    border-bottom: 1px dashed #d5d5d5;
}
.coupon-headblock .paper .dot-1,
.coupon-headblock .paper .dot-2,
.coupon-headblock .paper .dot-3,
.coupon-headblock .paper .dot-4,
.coupon-headblock .paper .dot-5,
.coupon-headblock .paper .dot-6 {
    height: 24rpx;
    width: 24rpx;
    border-radius: 24rpx;
    background: #f74a4a;
    position: absolute;
    top: -14rpx;
    left: 12rpx;
}
.coupon-headblock .paper .dot-2 {
    left: 48rpx;
}
.coupon-headblock .paper .dot-3 {
    left: 84rpx;
}
.coupon-headblock .paper .dot-4 {
    left: auto;
    right: 84rpx;
}
.coupon-headblock .paper .dot-5 {
    left: auto;
    right: 48rpx;
}
.coupon-headblock .paper .dot-6 {
    left: auto;
    right: 12rpx;
}
.coupon-headblock .paper .dot-top {
    height:80rpx;
    width:80rpx;
    border-radius:80rpx;
    position: absolute;
    top: -60rpx;
    left: 50%;
    margin-left: -40rpx;
    background: #f74a4a;
}
.coupon-headblock .paper .dot-left,
.coupon-headblock .paper .dot-right {
    height: 28rpx;
    width: 28rpx;
    border-radius: 28rpx;
    background: #f74a4a;
    position: absolute;
    top: 108rpx;
    left: -14rpx;
}
.coupon-headblock .paper .dot-right {
    left: auto;
    right: -14rpx;
}
.coupon-headblock .paper .title {
    line-height: 144rpx;
    text-align: center;
    display: block;
    font-size: 48rpx;
    color: #f74a4a;
}
.coupon-headblock .paper .text {
    height:160rpx;
    left: 20rpx;
    right: 20rpx;
    top: 142rpx;
    position: absolute;
    border: 1px solid #fad64f;
    text-align: center;
    display: block;
}
.coupon-headblock .paper .text .t1 {
    font-size: 36rpx;
    color: #eb3d3f;
    line-height: 58rpx;
    padding-top: 16rpx;
}
.coupon-headblock .paper .text .t1 span {
    font-size: 56rpx;
}
.coupon-headblock .paper .text .d1 {
    height: 28rpx;
    width: 28rpx;
    border-radius: 28rpx;
    border-style: solid;
    border-color: #fad64f transparent transparent transparent;
    border-width: 1px;
    background: #fff;
    position: absolute;
    top: -16rpx;
    left: -16rpx;
    transform:rotate(135deg);
}
.coupon-headblock .paper .text .d2 {
    height: 28rpx;
    width: 28rpx;
    border-radius: 28rpx;
    border-style: solid;
    border-color: #fad64f transparent transparent transparent;
    border-width: 1px;
    background: #fff;
    position: absolute;
    top: -16rpx;
    right: -16rpx;
    transform:rotate(-135deg);
}
.coupon-headblock .link-text {
    position: absolute;
    bottom: 158rpx;
    left: 50%;
    z-index: 6;
    width:360rpx;
    text-align: center;
    font-size: 28rpx;
    line-height:40rpx;
    color: #e47c48;
    margin-left: -180rpx;
}
.coupon-headblock .link-text a {
    color: #e47c48;
}
.coupon-groupblock {
    height: auto;
    overflow: hidden;
    margin: 20rpx;
    background: #fff;
    border-radius: 12rpx;
    border: 1.5px solid #dcdcdc;
    padding: 20rpx;
}
.coupon-groupblock .group-top {
    border-bottom: 1px dashed #d5d5d5;
    height: auto;
    overflow: hidden;
    padding-bottom: 20rpx;
}
.coupon-groupblock .group-top .inner {
    background: #f74a4a;
    float: left;
    color: #fff;
    padding: 0 8rpx;
    border-radius: 8rpx;
}
.coupon-groupblock .group-top .inner.blue {
    background: #42b5ff;
}
.coupon-groupblock .group-top .inner.pink {
    background: #f4558f;
}
.coupon-groupblock .group-top .inner.orange {
    background: #ff6c00;
}
.coupon-groupblock .group-top .inner.default {
    background: #bcbcbc;
}
.coupon-groupblock .group-top .inner .left {
    font-size: 56rpx;
    float: left;
}
.coupon-groupblock .group-top .inner .left span {
    font-size: 24rpx;
}
.coupon-groupblock .group-top .inner .right {
    float: left;
    padding-left: 12rpx;
    text-align: center;
}
.coupon-groupblock .group-top .inner .right .title {
    font-size: 32rpx;
    position: relative;
}
.coupon-groupblock .group-top .inner .right .title:before {
    content: "";
    position: absolute;
    height: 0;
    width: 100%;
    border-bottom: 1px solid #fff;
    left: 0;
    bottom: 2rpx;
}
.coupon-groupblock .group-top .inner .right .subtitle {
    font-size: 20rpx;
}
.coupon-groupblock .coupon-items {
    height:360rpx;
    background: #fff;
    overflow-y: hidden;
    overflow-x: auto;
    white-space: normal;
    position: relative;
    margin-top: 20rpx;
}
.coupon-groupblock .coupon-items .container1{
    z-index: -1;
    height: 376rpx;
    overflow: auto;
    white-space:nowrap;
}
.coupon-groupblock .coupon-items .item {
    height:360rpx;
    width:240rpx;
    overflow: hidden;
    text-decoration: none;
    color:#333;
    display: inline-block;
    font-size: 24rpx;
    margin-right: 8rpx;
    vertical-align:top;
}
.coupon-groupblock .coupon-items .item .image {
    height:240rpx;
    width:240rpx;
}
.coupon-groupblock .coupon-items .item .image image {
    height: 100%;
    width: 100%;
    border-radius: 8rpx;
    display: block;
}
.coupon-groupblock .coupon-items .item .title {
    height:40rpx;
    width:240rpx;
}
.coupon-groupblock .coupon-items .item .price .product {
    text-decoration: line-through;
    color: #999;
}
.coupon-groupblock .coupon-items .item .price .market {
    height: 28rpx;
    font-size: 28rpx;
    color: #fd5454;
    line-height: 28rpx;
}
.coupon-groupblock .coupon-items .item .price .market span {
    background: #fd5454;
    color: #fff;
    font-size: 22rpx;
    padding: 0 4rpx;
    border-radius: 4rpx;
    height:40rpx;
}
.coupon-groupblock .coupon-items .item .more {
    line-height:240rpx;
    background: #F4F4F4;
    text-align: center;
    font-size: 28rpx;
    color: #666;
    border-radius: 8rpx;
}


/*优惠券 */
.coupon-index-bg {
	background: #efeff4;
}

.coupon-index-list {
	padding: 32rpx 20rpx 20rpx;
}

.coupon-index-list-a {
	background: #fff;
	display: block;
	border-radius: 8rpx;
	overflow: hidden;
	margin-bottom: 20rpx;
}

.coupon-list {
	padding: 0;
	position: relative;
}

.coupon-index-list-left {
	position: relative;
	height: 240rpx;
}

.coupon-index-list-left>b {
	color: #fff;
	position: absolute;
	left: 24rpx;
	top: 0;
	height: 48rpx;
	line-height: 48rpx;
	font-weight: normal;
	font-size: 24rpx;
	border-bottom-left-radius: 8rpx;
	border-bottom-right-radius: 8rpx;
	padding: 0 20rpx;
}

.coupon-index-list-info {
	border: none;
	padding: 0 20rpx 0 32rpx;
	margin-top: 72rpx;
}

.coupon-index-list-left .fui-list:before {
	border: none;
}

.coupon-index-list-info .fui-list-media image {
	width: 140rpx;
	height: 140rpx;
	border: 2rpx solid #e6e6e6;
}

.coupon-index-list-info .fui-list-inner .h3 {
	font-size: 32rpx;
	color: #051b28;
	height: 60rpx;
	overflow: hidden;
	line-height: 60rpx;
  font-weight: 600;
}

.coupon-index-list-info .fui-list-inner .coupon-full,
.coupon-index-list-info .fui-list-inner .coupon-time {
	font-size: 24rpx;
	color: #999999;
	height: 40rpx;
	overflow: hidden;
}

.coupon-list>i {
	width: 24rpx;
	height: 24rpx;
	display: block;
	border-radius: 40rpx;
	background: #efeff4;
	position: absolute;
	z-index: 10;
}

.coupon-top-i {
	right: 148rpx;
	top: -12rpx;
}

.coupon-bot-i {
	right: 148rpx;
	bottom: -12rpx;
}

.coupon-list>span.coupon-ling {
	width: 160rpx;
	height: 160rpx;
	position: absolute;
	display: block;
	right: 40rpx;
	top: -24rpx;
	z-index: 9;
}

.coupon-list>span.coupon-ling image {
	width: 100%;
	height: 100%;
}

.coupon-index-list-right {
	width: 160rpx;
	height: 240rpx;
	display: block;
	margin: auto;
	color: #fff;
	padding: 20rpx 0 20rpx 0;
	text-align: center;
	border-radius: 8rpx;
}

.coupon-list-canvas {
	position: relative;
	text-align: center;
	display: block;
	height: 148rpx;
}

.coupon-list-canvas canvas {
	position: absolute;
	left: 12rpx;
	right: 40rpx;
	width: 136rpx;
}

.coupon-list-canvas strong {
	display: block;
}

.coupon-list-canvas p {
	display: block;
	padding-top: 20rpx;
	height: 60rpx;
	line-height: 40rpx;
	font-size: 28rpx;
	overflow: hidden;
}

.coupon-list-ling {
	display: inline-block;
	font-style: normal;
	font-size: 24rpx;
	height: 40rpx;
	line-height: 40rpx;
	border: 8rpx solid #cccaca;
	background: #fff;
	border-radius: 40rpx;
	color: #4dbaff;
	padding: 0 8rpx;
}

.coupon-list-ling.center {
	margin-top: 80rpx;
}

.coupon-index-list-info .fui-list-inner .coupon-full {
	height: 60rpx;
}

.coupon-full span {
	font-size: 40rpx;
	padding: 0 8rpx 0 0;
	font-weight: bold;
}

.coupon-time {
	font-size: 24rpx;
}

.coupon-time strong {
	font-weight: normal;
}

.blue .coupon-index-list-right {
	background: #42b5fe;
}

.blue .coupon-list-ling {
	border: 8rpx solid #13a1fa;
	color: #4dbaff;
}

.blue .coupon-index-list-left>b {
	background: #43b6ff;
}

.blue .coupon-index-list-info .fui-list-inner .coupon-full {
	color: #42b5fe;
}

.org .coupon-index-list-right {
	background: #ff6c00;
}

.org .coupon-list-ling {
	border: 8rpx solid #e65820;
	color: #ff7038;
}

.org .coupon-index-list-left>b {
	background: #ff6c00;
}

.org .coupon-index-list-info .fui-list-inner .coupon-full {
	color: #ff6c00;
}

.pink .coupon-index-list-right {
	background: #f4558f;
}

.pink .coupon-list-ling {
	border: 8rpx solid #dd2c6c;
	color: #f44b89;
}

.pink .coupon-index-list-left>b {
	background: #f55790;
}

.pink .coupon-index-list-info .fui-list-inner .coupon-full {
	color: #f55790;
}

.red .coupon-index-list-right {
	background: #f74a4a;
}

.red .coupon-list-ling {
	border: 8rpx solid #da363a;
	color: #f74a4a;
}

.red .coupon-index-list-left>b {
	background: #f74a4a;
}

.red .coupon-index-list-info .fui-list-inner .coupon-full {
	color: #f74a4a;
}

.disa .coupon-index-list-right {
	background: #bcbcbc;
}

.disa .coupon-index-list-left {
	background: #e5e5e5;
	-webkit-border-radius: 0.2rem;
	border-radius: 8rpx;
}

.disa .coupon-list-ling {
	border: 8rpx solid #cccaca;
	color: #848484;
	background: #e5e5e5;
}

.disa .coupon-index-list-left>b {
	background: #bcbcbc;
}

.disa .coupon-index-list-info .fui-list-inner .coupon-full {
	color: #bcbcbc;
}
</style>