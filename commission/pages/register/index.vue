<template>
<view>
<!--pages/commission/register/index.wxml-->
<loading v-if="!show">加载中...</loading>
<view class="page register" v-if="show">
    <view class="fui-content">
        <image :src="set['regbg']" mode="widthFix"></image>
    </view>
    <!--申请成为分销商-->
    <block v-if="member['status']==0 &&  member['isagent']==0 && set['become']==1">
        <view class="fui-cell-group">
            <view class="fui-cell-title">欢迎加入<text class="text-danger">{{ shopname }}</text>，请填写申请信息</view>
            <view class="fui-cell">
                <view class="fui-cell-label">邀请人</view>
                <view class="fui-cell-info"><text class="text-danger">{{ agent?agent['nickname']:'总店' }}</text>（请核对）</view>
            </view>
            <view class="fui-cell" v-if="hideicode == 0">
                <view class="fui-cell-label">{{set.texts.icode}}</view>
                <view class="fui-cell-info"><input type="text" class="fui-input" id="icode" :placeholder="'请填写' + set['texts']['icode']" :value="( mid > 0?mid:'' )" @input="inputChange"></input></view>
            </view>
             <include src="/pages/common/diyform.wxml"></include>

            <view class="fui-cell must" v-if="template_flag == 0">
                <view class="fui-cell-label">姓名</view>
                <view class="fui-cell-info"><input type="text" class="fui-input" id="realname" placeholder="请填写真实姓名,用于结算" :value="member.realname" @input="inputChange"></input></view>
            </view>
            <view class="fui-cell must" v-if="template_flag == 0">
                <view class="fui-cell-label">手机号</view>
                <view class="fui-cell-info"><input type="number" class="fui-input" id="mobile" placeholder="请填写手机号码,方便联系" :value="member.mobile" @input="inputChange"></input></view>
            </view>
        </view>

        <view class="btn btn-danger block btn-submit" @tap="submit">申请成为{{ set['texts']['agent'] }}</view>
       
        <view class="fui-list-group" v-if="set['register_bottom'] == ''">
            <view class="fui-list">
                <view class="fui-list-media">

                    <text class="icox icox-vip"></text>
                </view>
                <view class="fui-list-inner">
                    <view class="subtitle">{{ set['texts']['agent'] }}特权</view>
                </view>
            </view>

            <view class="fui-list">
                <view class="fui-list-media">
                              <text class="icox icox-erweima1" style="color: #feb312;"></text>
                </view>
                <view class="fui-list-inner">
                    <view class="subtitle">独立小店</view>
                    <view class="text">拥有自己的小店及推广二维码</view>
                </view>
            </view>

            <view class="fui-list">
                <view class="fui-list-media">
                    <text class="icox icox-qian" style="color:#ff5555"></text>
                </view>
                <view class="fui-list-inner">
                    <view class="subtitle">销售拿{{ set['texts']['commission'] }}</view>
                    <view class="text">成为{{ set['texts']['agent'] }}后卖出商品，您可以获得{{ set['texts']['commission'] }}</view>
                </view>
            </view>

            <view class="fui-list">
                <view class="fui-list-inner">
                    <view class="text">{{ set['texts']['agent'] }}的商品销售统一由厂家直接收款、直接发货，并提供产品的售后服务，{{ set['texts']['commission1'] }}由厂家统一设置。</view>
                </view>
            </view>
        </view>

        <view class="fui-list-group" v-if="set['register_bottom'] == '1'">
               <view class="fui-list" v-if="set['register_bottom_title1'] != '' && set['register_bottom_content1'] != ''">
                <view class="fui-list-media">
                              <text class="icox icox-vip"></text>
                </view>
                <view class="fui-list-inner">
                    <view class="subtitle">{{set['register_bottom_title1']}}</view>
                    <view class="text">{{set['register_bottom_content1']}}</view>
                </view>
            </view>


            <view class="fui-list" v-if="set['register_bottom_title2'] != '' && set['register_bottom_content2'] != ''">
                <view class="fui-list-media">
                              <text class="icox icox-erweima1" style="color: #feb312;"></text>
                </view>
                <view class="fui-list-inner">
                    <view class="subtitle">{{set['register_bottom_title2']}}</view>
                    <view class="text">{{set['register_bottom_content2']}}</view>
                </view>
            </view>

            <view class="fui-list" v-if="set['register_bottom_title3'] != '' && set['register_bottom_content3'] != ''">
                <view class="fui-list-media">
                    <text class="icox icox-qian" style="color:#ff5555"></text>
                </view>
                <view class="fui-list-inner">
                    <view class="subtitle">{{set['register_bottom_title3']}}</view>
                    <view class="text">{{set['register_bottom_content3']}}</view>
                </view>
            </view>

            <view class="fui-list" v-if="set['register_bottom_remark'] != ''">
                <view class="fui-list-inner">
                    <view class="text">{{ set['register_bottom_remark']}}</view>
                </view>
            </view>
        </view>

        <view class="fui-list-group" v-if="set['register_bottom'] == '2'">
            <view class="fui-list">
                <view class="fui-list-inner">
                    <rich-text :nodes="set['register_bottom_content']"></rich-text>
                </view>
            </view>
        </view>
    </block>

   <!--显示申请协议-->
    <view class="fui-list-group" v-if="set['open_protocol'] =='1' && set['applytitle'] !=''">  
      <view class="fui-list">
          <view class="fui-list-media">
                  <text class="icox icox-vip" style="color: #feb312;"></text>
          </view>
          <view class="fui-list-inner">
              <view class="subtitle">{{ set['applytitle'] }}</view>
          </view>   
      </view>
      <view class="fui-list">
          <view class="fui-list-inner">
          <rich-text :nodes="set['applycontent']"></rich-text>
          </view>    
      </view>        
    </view>
<!--消费次数-->
    <block v-if="set['become']==2 && status==0">
    <view class="fui-list-group">
        <view class="fui-list-group-title">
            <image src="/static/images/icon/nolist.png"></image>
            <text class="remind">友情提醒</text>
        </view>
        <view class="fui-list">
            <view class="fui-list-inner">
                <view class="text">本店累计消费满 <text class="text-danger text-bold">{{ order_totalcount }}</text>次，才可成为<text class="text-danger text-bold">{{ shopname }}</text>购物中心分销商，您已消费<text class="text-danger text-bold">{{ order_count }}</text>次，请继续努力！</view>
            </view>
        </view>
    </view>
    <navigator class="btn btn-danger block" url="/pages/index/index" open-type="switchTab">继续去购物</navigator>
    </block>


    <!--消费金额-->
    <block v-if="set['become']==3 && status==0">
    <view class="fui-list-group">
        <view class="fui-list-group-title">
            <image src="/static/images/icon/nolist.png"></image>
            <text class="remind">友情提醒</text>
        </view>
        <view class="fui-list">
            <view class="fui-list-inner">
                <view class="text">本店累计消费满 <text class="text-danger text-bold">{{ money_totalcount }}</text>{{ set['texts']['yuan'] }}，才可成为<text class="text-danger text-bold">{{ shopname }}</text>购物中心分销商，您已消费<text class="text-danger text-bold">{{ moneycount }}</text>{{ set['texts']['yuan'] }}，请继续努力！</view>
            </view>
        </view>
    </view>
    <navigator class="btn btn-danger block" url="/pages/index/index" open-type="switchTab">继续去购物</navigator>
    </block>



<!--购买特定商品-->
    <block v-if="set['become']==4 && status==0 && member['isagent']==0">
    <view class="fui-list-group">
        <view class="fui-list-group-title">
            <image src="/static/images/icon/nolist.png"></image>
            <text class="remind">友情提醒</text>
        </view>
        <navigator :url="'/pages/goods/detail/index?id=' + buy_goods['id']">
            <view class="fui-list">
                <view class="fui-list-media">
                    <image :src="buy_goods['thumb']"></image>
                </view>
                <view class="fui-list-inner">
                    <view class="text">{{ buy_goods['title'] }}</view>
                    <view class="text">{{ buy_goods['marketprice'] }}</view>
                </view>
            </view>
        </navigator>
        <view class="fui-list">
                <view class="fui-list-inner">
                    <view class="text">本店需购买此商品才可成为<text class="text-danger text-bold">{{ shopname }}</text>购物中心{{ set['texts']['agent'] }}，请现在去购买吧！</view>
                </view>
        </view>
    </view>
     <navigator class="btn btn-danger block" :url="'/pages/goods/detail/index?id=' + buy_goods['id']">现在就去购买</navigator>
    </block>

     <!--提交申请等待-->
    <block v-if="member['status']==0 && member['isagent']==1">
     <view class="wait">
        <image src="/static/images/icon/wait-128.png"></image>
        <view>谢谢您的支持，请等待审核！</view>
        <navigator class="btn btn-danger" url="/pages/index/index" open-type="switchTab">去商城逛逛</navigator>
     </view>
    </block>
</view>
<navigator class="commission-shouye" url="/pages/index/index" open-type="switchTab">
  <text class="icox icox-shouye"></text>
</navigator>
<include src="/pages/common/city-picker.wxml"></include>
<view :class="'fui-mask ' + ( showPicker?'show':'' )"></view>
</view>
</template>

<script>

export default {
  data() {
    return {};
  },

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
@import "../../../pages/common/city-picker.css"; 
.register .fui-list-group .fui-list .image-32{
    width: 32rpx;
    height: 32rpx
} 
.fui-list-group .fui-list-inner{
    font-size: 30rpx
}
.register .fui-content image{
    width: 100%;
    height: 242rpx
}
.remind{
    margin-top: 12rpx
}
.wait{
    text-align: center
}
.commission-shouye{
  position: fixed;
  right: 20rpx;
  z-index: 999;
  font-size: 22rpx;
  color:#fff;
  width: 84rpx;
  height:84rpx;
  transition: all .7s;
  -moz-transition: all .7s; /* Firefox 4 */
  -webkit-transition: all .5s; /* Safari å’Œ Chrome */
  -o-transition: all .5s; /* Opera */
  background: rgba(0, 0, 0, 0.5);
  bottom: 280rpx;

  
}
.commission-shouye {
  width: 90rpx;
  height: 90rpx;
  background: #ff5555;
  position: fixed;
  right: 20rpx;
  bottom: 80rpx;
  border-radius: 50%;
  text-align: center;
  padding: 0;
  line-height: 90rpx;
}
.commission-shouye {
  bottom: 190rpx;
}
.commission-shouye .icox{
  font-size: 50rpx;
  color: #fff
}

.wait image{
    width: 220rpx;
    height:220rpx;
    margin: 50rpx 0
}
.wait view{
    margin: 20rpx;
    color:#666
}
</style>