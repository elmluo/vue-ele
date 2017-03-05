<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avator">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="discription">
          {{seller.description}} / {{seller.deliveryTime}}分钟送达
        </div>
        <div class="supports" v-if="seller.supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="supports-count" @click="showDetail()">
        <span class="count">{{seller.supports.length}}个 &gt;</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="notice-wrapper">
      <span class="notice-title"></span><span class="notice-text">{{seller.notice}}</span>
      <i class="icon-keyboard_arrow_right"> &gt;</i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-content-wrapper clearfix">
        <div class="detail-content">
          <h1 class="name">{{seller.name}}</h1>
          <div class="star-wrapper">
            <v-star :size="48" :score="seller.score"></v-star>
          </div>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <ul class="supports" v-if="seller.supports">
            <li class="supports-item" v-for="item in seller.supports" >
              <span class="icon" :class="classMap[$index]"></span>
              <span class="text">{{seller.supports[$index].description}}</span>
            </li>
          </ul>
          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>
          <div class="notice">
            <p class="content">{{seller.notice}}</p>
          </div>
        </div>
      </div>
      <div class="detail-close">
        <i class="icon-close">X</i>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from 'components/star/star.vue';

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailShow: false
      };
    },
    methods: {
      showDetail: function () {
        this.detailShow = true;
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    components: {
      'v-star': star
    }
  };

</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl";

  .header
    position: relative
    color: rgb(255, 255, 255)
    background-color: rgba(7, 17, 2, 0.5)
    .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avator
        display: inline-block
        img
          border-radius: 2px
      .content
        vertical-align: top
        display: inline-block
        margin-left: 16px
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-weight: blod
            line-heigth: 18px
            font-size: 20px
        .discription
          margin-bottom: 10px
          font-size: 12px
          line-height 12px
        .supports
          .icon
            display: inline-block
            vertical-align top
            width: 12px
            height: 12px
            margin-right: 4px
            background-size 12px 12px
            background-repeat no-repeat
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.special
              bg-image('special_1')
            &.invoice
              bg-image('invoice_1')
            &.guarantee
              bg-image('guarantee_1')
          .text
            font-size: 12px
      .supports-count
        position: absolute
        right: 12px
        bottom: 18px
        padding: 0 8px
        height: 24px
        line-height: 24px
        border-radius: 14px
        background-color: rgba(0, 0, 0, 0.2)
        text-align: center
        .count
          font-size: 12px
        .icon-keyboard_arrow_right
          font-size: 10px
    .notice-wrapper
      position: relative
      height: 28px
      line-height: 28px
      padding: 0 22px 0 12px
      white-space: nowrap
      text-overflow: ellipsis
      overflow: hidden
      background-color: rgba(7, 17, 27, 0.2)
      .notice-title
        display: inline-block
        width: 22px
        height: 12px
        margin-top: 8px
        bg-image('notice')
        background-size: 22px
        background-repeat: no-repeat
        vertical-align: top
      .notice-text
        vertical-align: top
        margin: 0 4px
        font-size: 12px
      .icon-keyboard_arrow_right
        position: absolute
        top: 7px
        right: 12px
        font-size: 12px
    .background
      position: absolute
      top: 0
      bottom: 0
      left: 0
      right: 0
      z-index: -1
      filter: blur(10px)
    .detail
      position: fixed
      top: 0
      left: 0
      z-index: 100
      width: 100%
      height: 100%
      overflow: auto
      background: rgba(7, 17, 27, 0.8)
      .detail-content-wrapper
        min-height: 100%
        width: 100%
        .detail-content
          margin-top: 64px
          padding-bottom: 64px
          .name
            font-size: 16px
            text-align: center
            font-weight: 700
            line-height: 16px
          .star-wrapper
            margin-top: 18px
            padding: 2px 0
            text-align: center
          .title
            display: flex
            margin: 28px auto 24px auto
            width: 80%
            .text
              padding: 0 12px
              font-size: 14px
              font-weight: 700
            .line
              flex: 1;
              position: relative
              top: 6px
              border-top: 1px solid rgba(255,255,255,0.2)
          .supports
            width: 80%
            margin: 24px auto 28px auto
            .supports-item
              margin: 12px
              font-size: 0
              .icon
                display: inline-block
                vertical-align: top
                margin-right: 6px
                width: 16px
                height: 16px
                background-size: 16px
                background-repeat: no-repeat
                &.decrease
                  bg-image('decrease_2')
                &.discount
                  bg-image('discount_2')
                &.special
                  bg-image('special_2')
                &.invoice
                  bg-image('invoice_2')
                &.guarantee
                  bg-image('guarantee_2')
              .text
                display: inline-block
                line-height: 16px
                font-size: 14px
                font-weight: 100
          .notice
            width: 80%
            margin: 24px auto 28px auto
            .content
              margin: 12px
              font-size: 14px
              line-height: 24px
      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        font-size: 32px
</style>
