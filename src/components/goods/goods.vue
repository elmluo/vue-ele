<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" class="menu-item border-1px">
          <span class="text">
            <span class="icon" v-show="item.type>0" :class="classMap[item.type]"></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foots-wrapper"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  const ERR_OK = 0;

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
      this.$http.get('./api/goods').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.goods = response.data;
//          console.log(this.goods);
        }
      });
    },
    data() {
      return {
        goods: []
      };
    }

  };

</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"

  .goods
    display: flex
    position absolute
    top 174px
    bottom: 46px
    width: 100%
    overflow: hidden
    .menu-wrapper
      flex: 0 0 80px
      width: 80px
      background: #f3f5f7
      .menu-item
        diaplay: table
        padding: 0 12px
        width: 56px
        height: 54px
        line-height: 14px
        .icon
          display: inline-block
          vertical-align top
          width: 12px
          height: 12px
          margin-right: 2px
          background-size 12px 12px
          background-repeat no-repeat
          &.decrease
            bg-image('decrease_3')
          &.discount
            bg-image('discount_3')
          &.special
            bg-image('special_3')
          &.invoice
            bg-image('invoice_3')
          &.guarantee
            bg-image('guarantee_3')
        .text
          display: table-cell
          width: 56px
          vertical-align: middle
          font-size: 14px
          border-1px(rgba(7, 17, 27, 0.1))
    .foots-wrapper
      flex: 1

</style>
