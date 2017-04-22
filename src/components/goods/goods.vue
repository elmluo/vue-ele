<template>
  <div class="goods">
    <div class="menu-wrapper" v-el:menu-wrapper>
      <ul>
        <li v-for="item in goods" class="menu-item border-1px" :class="{'current': currentIndex==$index}">
          <span class="text">
            <span class="icon" v-show="item.type>0" :class="classMap[item.type]"></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foots-wrapper" v-el:foods-wrapper>
      <ul>
        <li v-for="item in goods" class="food-list food-list-hook">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item border-1px">
              <div class="icon">
                <img :src="food.icon" width="57" height="57">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll';
  const ERR_OK = 0;

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    computed: {
      /**
       * 计算属性（自己执行）：添加索引
       *    根据滚动scrollY的值，判断在哪个栏目所在的高度范围之内，返回对应index
       *    根据vue的计算属性特性，scrollY实时变化，currentIndex也会实时变化。
       */
      currentIndex() {
        for (let i = 0; i < this.listHeight.length - 1; i++) {
          let height1 = this.listHeight[i];
          let heigth2 = this.listHeight[i + 1];
          if (!heigth2 || (this.scrollY > height1 && this.scrollY < heigth2)) {
            return i;
          }
        }
        return 0;
      }
    },
    created() {
      // 获取数据在DOM跟新之前
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];

      /**
       * 在创建的生命周期时候时候获取数组
       */
      this.$http.get('./api/goods').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.goods = response.data;
//          console.log(this.goods);

          // 拿到数据以后DOM跟新，然后再去计算高度
          this.$nextTick(() => {
            this._initScroll();
            this._calculateHeight();
//            console.log(123);
          });
        }
      });
    },
    data() {
      return {
        goods: [],

        // 定义一个数组，用来存高度的变量
        listHeight: [],

        // 定义一个需要跟踪的一个变量
        scrollY: 0
      };
    },
    methods: {
      /**
       * 使用滚动插件
       */
      _initScroll() {
        this.menuScroll = new BScroll(this.$els.menuWrapper, {});
        this.foodsScroll = new BScroll(this.$els.foodsWrapper, {
          // 开启插件实时滚动监听功能
          probeType: 3
        });
        // 监听scrollY值的变化
        this.foodsScroll.on('scroll', (pos) => {
          this.scrollY = Math.abs(Math.round(pos.y));
        });
      },

      /**
       * 计算右侧每个栏目列表高度，存入data中定义的listHeight数组
       * @type {NodeList}
       */
      _calculateHeight() {
        // 找到该组件下的foodlist元素
        let foodList = this.$els.foodsWrapper.getElementsByClassName('food-list-hook');
        console.log(foodList);
        let height = 0;
        for (let i = 0; i < foodList.length; i++) {
          console.log(foodList.length);
          height += foodList[i].clientHeight;
          console.log(foodList[i]);
          this.listHeight.push(height);
          console.log(this.listHeight);
        }
      }
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
        display: table
        padding: 0 12px
        width: 56px
        height: 54px
        line-height: 14px
        &.current
          position: relative
          z-index: 10;
          margin-top: -1px
          background: #00ff00
          font-weight: 700
          .text
            border-none()
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
      .title
        padding-left: 14px
        height: 26px
        line-height: 26px
        border-left: 2px solid #d9dde1
        font-size: 12px
        color: rgb(147, 153, 159)
        background: #f3f5f7
      .food-item
        display: flex
        margin: 18px
        padding-bottom: 18px
        border-1px(rgba(7, 17, 27, 0.1))
        &:last-child
          border-none()
          margin-bottom: 0px
        .icon
          flex: 0 0 57px
          margin-right: 10px
        .content
          flex: 1
          .name
            margin: 2px 0 8px 0
            height: 14px
            line-height: 14px
            font-size: 14px
            color: rgb(7, 17, 27)
          .desc, .extra
            line-height: 10px
            font-size: 10px
            color: rgb(147, 153, 159)
          .desc
            margin-bottom: 8px
            line-height: 12px
          .extra
            line-height: 10px
            &.count
              padding-right: 12px
          .price
            font-weight: 700px
            line-height: 24px
            .now
              margin-right: 18px
              font-size: 14px
              color: rgb(240, 20, 20)
            .old
              text-decoration: line-through
              font-size: 10px
              color: rgb(147, 153, 159)
</style>
