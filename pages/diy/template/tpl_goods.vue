<template>
<view>
<view :class="'fui-goods-group ' + diyitem.style.liststyle" v-if="diyitem.params.goodsscroll!=1" :style="'background:' + diyitem.style.background">
    <view class="fui-goods-item" v-for="(childitem, index) in diyitem.data" :key="index">
        <navigator :url="( childitem.bargain > 0?'../../../bargain/detail/detail?id='+childitem.bargain : '/pages/goods/detail/index?id='+childitem.gid)" :class="'image ' + (diyitem.params.showicon=='1'?diyitem.style.iconstyle:'')" :data-text="diyitem.style.goodsicon" :style="'background-image:url(' + (diyitem.params.showicon=='2'?diyitem.params.goodsiconsrc:childitem.thumb) + ')'">
        
        <!--营销图标  -->
            <view class="goodsicon" v-if="diyitem.params.showicon=='2'" :style="'position:relative;width:' + iconwidth + 'px;height:' + iconheight + 'px'">
                <image wx-if="{{diyitem.params.iconposition=="left top"}}" class="left top" mode="widthFix" :src="diyitem.params.goodsiconsrc" :style="'width:' + diyitem.style.iconzoom + '%; left:' + diyitem.style.iconpaddingleft + 'rpx;top:' + diyitem.style.iconpaddingtop + 'rpx'" @load="goodsicon"></image>
                <image wx-if="{{diyitem.params.iconposition=="right top"}}" class="right top" mode="widthFix" :src="diyitem.params.goodsiconsrc" :style="'width:' + diyitem.style.iconzoom + '%; right:' + diyitem.style.iconpaddingleft + 'rpx;top:' + diyitem.style.iconpaddingtop + 'rpx'" @load="goodsicon"></image>
                <image wx-if="{{diyitem.params.iconposition=="left bottom"}}" class="left bottom" mode="widthFix" :src="diyitem.params.goodsiconsrc" :style="'width:' + diyitem.style.iconzoom + '%; left:' + diyitem.style.iconpaddingleft + 'rpx;bottom:' + diyitem.style.iconpaddingtop + 'rpx'" @load="goodsicon"></image>
                <image wx-if="{{diyitem.params.iconposition=="right bottom"}}" class="right bottom" mode="widthFix" :src="diyitem.params.goodsiconsrc" :style="'width:' + diyitem.style.iconzoom + '%; right:' + diyitem.style.iconpaddingleft + 'rpx;bottom:' + diyitem.style.iconpaddingtop + 'rpx'" @load="goodsicon"></image>
            </view>
            <!--售罄  -->
            <image class="salez" :src="(diyitem.params.saleout == 0?'/static/images/saleout-2.png':diyitem.params.saleout)" v-if="(diyitem.params.saleout!=-1 && childitem.total==0 && childitem.cansee<=0) || (diyitem.params.saleout!=-1 && childitem.total==0 && childitem.cansee>0 &&  childitem.seecommission<=0)"></image>
           <!--分销佣金  -->
            <view v-if="childitem.cansee>0 && childitem.seecommission>0" class="goods-Commission">{{childitem.seetitle}}￥{{childitem.seecommission}}</view>        
        </navigator>
        <view class="detail">
            <navigator :url="( childitem.bargain > 0?'../../../bargain/detail/detail?id='+childitem.bargain : '/pages/goods/detail/index?id='+childitem.gid)" class="name" wx-if="{{diyitem.params.showtitle=="1"}}" :style="'color:' + diyitem.style.titlecolor">
            <image src="/static/images/label.png" class="bargain_label" v-if="childitem.bargain > 0"></image>
             <text class="cycle-tip" v-if="childitem.ctype == 9">周期购</text> 
            <text>{{childitem.title}} </text>   
            </navigator>
            <!--原价销量  -->
            <view class="productprice" v-if="diyitem.params.showprice=='1' && (diyitem.params.showproductprice=='1'|| diyitem.params.showsales=='1')">
                 <text :style="'color:' + diyitem.style.productpricecolor + ';margin-right:16rpx'" v-if="childitem.productprice>0 && diyitem.params.showproductprice=='1'">{{diyitem.params.productpricetext}}：<text :class="(diyitem.params.productpriceline=='1'?'line':'')">￥{{childitem.productprice}}</text>
                 </text>
                 <text v-if="diyitem.params.showsales=='1'" :style="'color:' + diyitem.style.salescolor">{{diyitem.params.salestext}}：{{childitem.sales}}</text>
            </view>
            <!--价格购买按钮  -->
            <view class="price" wx-if="{{diyitem.params.showprice=="1"}}">
                <text class="text" :style="'color:' + diyitem.style.pricecolor">￥{{childitem.price}}</text>
                <navigator class="buy buybtnbtn buybtn-1" wx-if="{{childitem.ctype == 9 && childitem.bargain == 0}}" style :url="'/pages/goods/detail/index?id=' + childitem.gid" data-buytype="buy" :data-id="childitem.gid">详情</navigator>
                <navigator class="buy buybtnbtn buybtn-1" wx-if="{{childitem.ctype == 5 && childitem.bargain == 0}}" style :url="'/pages/goods/detail/index?id=' + childitem.gid" data-buytype="buy" :data-id="childitem.gid">详情</navigator>
                <navigator class="buy buybtnbtn buybtn-1" wx-if="{{childitem.bargain > 0}}" style :url="'../../../bargain/detail/detail?id=' + childitem.bargain" data-buytype="buy" :data-id="childitem.gid">砍价</navigator>
                <text :class="'buy buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-1' && childitem.ctype != 9 && (childitem.bargain == 0 || childitem.bargain == null ) && childitem.ctype != 5}}" :style="'color:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitem.gid" data-home="1">购买</text>
                <text :class="'buy buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-2' && childitem.ctype != 9 && (childitem.bargain == 0 || childitem.bargain == null ) && childitem.ctype != 5}}" :style="'background:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitem.gid" data-home="1">购买</text>
                <text :class="'buy icox icox-cartfill buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-3' && childitem.ctype != 9 && childitem.ctype != 5 && childitem.bargain == 0}}" :style="'background:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitem.gid"></text>
                <text :class="'buy icox icox-gouwuche4 buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-4' && childitem.ctype != 9 && childitem.ctype != 5 && childitem.bargain == 0}}" :style="'color:' + diyitem.style.buybtncolor + ';'" @tap="selectPicker" data-buytype="buy" :data-id="childitem.gid"></text>
                <text :class="'buy icox icox-add buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-5' && childitem.ctype != 9 && childitem.ctype != 5 && childitem.bargain == 0}}" :style="'color:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitem.gid"></text>
                <text :class="'buy icox icox-add buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-6' && childitem.ctype != 9 && childitem.ctype != 5 && childitem.bargain == 0}}" :style="'background:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitem.gid"></text>
            </view>
        </view>  
    </view>
</view>

<!--商品轮播  -->
<view class="fui-goods-swiper-group" style="position: relative;" v-if="diyitem.params.goodsscroll==1">
<view class="cut retreat" @tap="cutGoods" :data-id="diyitemid" :data-num="diyitem.data_temp.length" data-type="retreat"><i class="icox icox-qianjin-copy-copy"></i></view>
<swiper :class="'swiper fui-goods-group ' + diyitem.style.liststyle + ' ' + (diyitem.params.showprice=='1' && (diyitem.params.showproductprice=='1'|| diyitem.params.showsales=='1')?'showproduct':'') + ' ' + (diyitem.params.showtitle==1?'showtitle':'') + ' ' + (diyitem.params.showprice==1?'showprice':'')" circular="true" :interval="interval" :duration="duration" :current="diyitem.current" :style="'background:' + diyitem.style.background + ';'" v-if="diyitem.params.goodsscroll==1">
  <block>
    <swiper-item v-for="(childitem, index) in diyitem.data_temp" :key="index" next-margin="10px">
       <view class="fui-goods-item" v-for="(childitems, index2) in childitem" :key="index2">
        <navigator :url="( childitems.bargain > 0?'../../../bargain/detail/detail?id='+childitems.bargain : '/pages/goods/detail/index?id='+childitems.gid)" open-type="navigate" :class="'image ' + (diyitem.params.showicon=='1'?diyitem.style.iconstyle:'')" :data-text="diyitem.style.goodsicon" :style="'background-image:url(' + (diyitem.params.showicon=='2'?diyitem.params.goodsiconsrc:childitems.thumb) + ')'">
        <!--营销图标 -->
            <view class="goodsicon" v-if="diyitem.params.showicon=='2'" :style="'position:relative;width:' + iconwidth + 'px;height:' + iconheight + 'px'">
                <image wx-if="{{diyitem.params.iconposition=="left top"}}" class="left top" mode="widthFix" :src="childitem.thumb" :style="'width:' + diyitem.style.iconzoom + '%; left:' + diyitem.style.iconpaddingleft + 'rpx;top:' + diyitem.style.iconpaddingtop + 'rpx'" @load="goodsicon"></image>
                <image wx-if="{{diyitem.params.iconposition=="right top"}}" class="right top" mode="widthFix" :src="childitem.thumb" :style="'width:' + diyitem.style.iconzoom + '%; right:' + diyitem.style.iconpaddingleft + 'rpx;top:' + diyitem.style.iconpaddingtop + 'rpx'" @load="goodsicon"></image>
                <image wx-if="{{diyitem.params.iconposition=="left bottom"}}" class="left bottom" mode="widthFix" :src="childitem.thumb" :style="'width:' + diyitem.style.iconzoom + '%; left:' + diyitem.style.iconpaddingleft + 'rpx;bottom:' + diyitem.style.iconpaddingtop + 'rpx'" @load="goodsicon"></image>
                <image wx-if="{{diyitem.params.iconposition=="right bottom"}}" class="right bottom" mode="widthFix" :src="childitem.thumb" :style="'width:' + diyitem.style.iconzoom + '%; right:' + diyitem.style.iconpaddingleft + 'rpx;bottom:' + diyitem.style.iconpaddingtop + 'rpx'" @load="goodsicon"></image>
            </view>
            <!--售罄  -->
            <image class="salez" :src="(diyitem.params.saleout == 0?'/static/images/saleout-2.png':diyitem.params.saleout)" v-if="(diyitem.params.saleout!=-1 && childitems.total==0 && childitems.cansee<=0) || (diyitem.params.saleout!=-1 && childitems.total==0 && childitems.cansee>0 &&  childitems.seecommission<=0)"></image>
           <!--分销佣金  -->
            <view v-if="childitems.cansee>0 && childitems.seecommission>0" class="goods-Commission">{{childitems.seetitle}}￥{{childitems.seecommission}}</view>        
        </navigator>
        <view class="detail">
            <navigator :url="( childitems.bargain > 0?'../../../bargain/detail/detail?id='+childitems.bargain : '/pages/goods/detail/index?id='+childitems.gid)" open-type="navigate" class="name" wx-if="{{diyitem.params.showtitle=="1"}}" :style="'color:' + diyitem.style.titlecolor">
                {{childitems.title}}
            </navigator>
            <!--原价销量  -->

          <view class="productprice" v-if="diyitem.params.showprice=='1' && (diyitem.params.showproductprice=='1'|| diyitem.params.showsales=='1')">
         
                 <text :style="'color:' + diyitem.style.productpricecolor + ';margin-right:16rpx'" v-if="childitems.productprice>0 && diyitem.params.showproductprice=='1'">{{diyitem.params.productpricetext}}：<text :class="(diyitem.params.productpriceline=='1'?'line':'')">￥{{childitems.productprice}}</text>
                 </text>
                 <text v-if="diyitem.params.showsales=='1'" :style="'color:' + diyitem.style.salescolor">{{diyitem.params.salestext}}:  {{childitems.sales}}</text>
            </view>
            <!--价格购买按钮  -->
            <view class="price" wx-if="{{diyitem.params.showprice=="1"}}">
                <text class="text" :style="'color:' + diyitem.style.pricecolor">￥{{childitems.price}}</text>
                <text :class="'buy buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-1'}}" :style="'color:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitems.gid" data-home="1">购1买</text>
                <text :class="'buy buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-2'}}" :style="'background:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitems.gid" data-home="1">购买</text>
                <text :class="'buy icox icox-cartfill buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-3'}}" :style="'background:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitems.gid"></text>
                <text :class="'buy icox icox-gouwuche4 buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-4'}}" :style="'color:' + diyitem.style.buybtncolor + ';'" @tap="selectPicker" data-buytype="buy" :data-id="childitems.gid"></text>
                <text :class="'buy icox icox-add buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-5'}}" :style="'color:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitems.gid"></text>
                <text :class="'buy icox icox-add buybtnbtn ' + diyitem.style.buystyle" wx-if="{{diyitem.style.buystyle=='buybtn-6'}}" :style="'background:' + diyitem.style.buybtncolor + ';border-color:' + diyitem.style.buybtncolor" @tap="selectPicker" data-buytype="buy" :data-id="childitems.gid"></text>
            </view>
        </view>  
    </view>
    </swiper-item>
  </block>

</swiper>
  <view class="cut advance" @tap="cutGoods" :data-id="diyitemid" :data-num="diyitem.data_temp.length" data-type="advance"><i class="icox icox-qianjin-copy"></i></view>
  </view>
</view>
</template>


	<script> 
		
		export default {
			props: []
		}
	</script> 
									