<template>
<view>
<!-- 样式一 -->
<view style="overflow: hidden;height: 360rpx;position: relative;background: #fff" v-if="diyitem.params.style=='default1'">
    <view class="member-head" style="z-index:100;border: none;"> 
        <view class="child">
            <view class="title" :style="'color:' + diyitem.style.textcolor|| ''">{{member.moneytext}}</view>
            <view class="number" :style="'color:' + diyitem.style.textlight|| ''">{{member.credit2}}</view>
            <navigator :url="diyitem.params.leftnavlink" class="btn" hover-class="btn-hover" v-if="member.open_recharge" open-type="navigate" :style="'color:' + diyitem.style.textcolor|| '' + ';border-color:' + diyitem.style.textcolor|| ''">{{diyitem.params.leftnav}}</navigator>
        </view>
        <view class="child userinfo">
            <view :class="'avatar ' + diyitem.style.headstyle || ''">
                <image class="icon" :src="member.avatar||'/static/images/noface.png'"></image>
            </view>
            <view class="nickname" :style="'color:' + diyitem.style.textcolor|| ''">{{member.nickname}}</view>
            <view class="level" :style="'color:' + diyitem.style.textcolor|| ''">{{member.levelname}}<navigator v-if="diyitem.params.levellink != '' &&  diyitem.params.levellink != undefined" :url="diyitem.params.levellink" style="display:inline-block"><i class="icox icox-feedback"></i></navigator></view>
        </view>
    <view class="child">
      <view class="title" :style="'color:' + diyitem.style.textcolor|| ''">{{member.credittext}}</view>
      <view class="number" :style="'color:' + diyitem.style.textlight|| ''">{{member.credit1}}</view>
      <navigator v-if="member.open_creditshop == 1" :url="diyitem.params.rightnavlink" class="btn" hover-class="btn-hover" :style="'color:' + diyitem.style.textcolor|| '' + ';border-color:' + diyitem.style.textcolor|| ''">{{diyitem.params.rightnav}}</navigator>
    </view>
  </view>
  <view class="member_header" :style="'background:' + diyitem.style.background + ';border-color:' + diyitem.style.background"></view>
  <block v-if="member.usemembercard">
    <navigator hover-class="none" open-type="navigate" :url="'/pages/member/membercard/index?hasmembercard=' + member.hasmembercard" class="member_card">
      <image src="/static/images/icon-huangguan.png" class="icon"></image>
      <view class="title">我的会员卡</view>
      <view class="card-num">已拥有{{member.hasbuycardnum}}张</view>
    </navigator>
    <image src="/static/images/cover.png" class="cover-img"></image>
  </block>
</view>
<!--样式二  -->
<view class="headinfo style-2" :style="'background:' + diyitem.style.background + ';'" v-else>
  <navigator class="icon-style2" hover-class="none" open-type="navigate" :url="'/pages/member/membercard/index?hasmembercard=' + member.hasmembercard" v-if="member.usemembercard">
    <image src="/static/images/header-style2.png"></image>
  </navigator>

  <navigator class="setbtn" :url="diyitem.params.setlink">
    <i :class="'icox ' + diyitem.params.seticon"></i>
  </navigator>
  <view :class="'face ' + diyitem.style.headstyle || ''">
    <image class="icon" :src="member.avatar||'/static/images/noface.png'"></image>
  </view>
  <view class="inner">
    <view class="name" :style="'color:' + diyitem.style.textcolor|| ''">{{member.nickname}}</view>
    <view class="level" :style="'color:' + diyitem.style.textcolor|| ''">{{member.levelname}}</view>
    <view class="credit" :style="'color:' + diyitem.style.textcolor|| ''">{{member.moneytext}} :
      <text :style="'color:' + diyitem.style.textlight|| ''">{{member.credit2}}</text>
    </view>
    <view class="credit" :style="'color:' + diyitem.style.textcolor|| ''">{{member.credittext}} :
      <text :style="'color:' + diyitem.style.textlight|| ''">{{member.credit1}}</text>
    </view>
  </view>
</view>
</view>
</template>


	<script> 
		
		export default {
			props: []
		}
	</script> 
									