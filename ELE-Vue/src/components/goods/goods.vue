<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menuWrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
            <span class="text" border-1px>
              <span v-show="item.type > 0"  class="menu-icon" :class="classMap[item.type]"></span>
              {{item.name}}
            </span>
        </li>
      </ul>cd
    </div>
    <div class="foots-wrapper" ref="footsWrapper" >
      <ul>
        <li v-for="item in goods" class="food-list">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item">
              <div class="icon">
                <img width="57" height="57" src="" :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}} </p>
                <div class="extra">
                  <span>月售{{food.sellCount}}份 </span>
                  <span class="goodRate">好评率 {{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="newPrice">￥{{food.price}}</span>
                  <span class="oldPrice" v-show="food.oldPrice">￥{{food.oldPrice}} </span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6" >
const ERR_OK = 0;

export default {
  props: {
    seller: {
      type: Object
    }
  },
  data: function(){
    return {
      goods: []
    }
  },
  created: function(){
      this.classMap = ['decrease','discount','guarantee','invoice','special'];
      this.$http.get('/api/goods').then((response) => {
        response = response.body;
        if(response.errno === ERR_OK){
          this.goods = response.data;
        }
    })
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/index.styl';
  @import '../../common/stylus/mixin.styl';
  
  .goods
    display: flex
    position: absolute
    top: 177px
    bottom: 46px
    width: 100%
    overflow: hidden
    .menu-wrapper
      flex: 0 0 80px
      background-color: #f3f5f7
      .menu-item
        display: table
        height: 54px
        width: 56px
        padding: 0 12px
        line-height: 14px
    .foods-wrapper
      flex: 1
    .title
      padding-left: 14px
      height: 26px
      line-height: 26px
      border-left: 2px solid #d9dde1
      font-size: 12px
      color: rgb(147,153,159)
      background: #f3f5f7
    .food-item
      display: flex
      padding: 18px
      border-1px(rgba(7,17,27,0.1))
    .menu-icon
      display: inline-block
      vertical-align: top
      width: 12px
      height: 12px
      margin-right: 2px 
      background-size: 12px 12px
      background-repeat: no-repeat
      &.decrease
        bg-image('decrease_3')
      &.discount
        bg-image('discount_3')    
      &.guarantee
        bg-image('guarantee_3') 
      &.invoice
        bg-image('invoice_3')
      &.special
        bg-image('special_3')
    .icon
      display: inline-block
      vertical-align: top
      margin-right: 10px 
      background-size: 12px 12px
      background-repeat: no-repeat
      &.decrease
        bg-image('decrease_3')
      &.discount
        bg-image('discount_3')    
      &.guarantee
        bg-image('guarantee_3') 
      &.invoice
        bg-image('invoice_3')
      &.special
        bg-image('special_3')
    .text
      display: table-cell
      vertical-align: middle 
      font-size: 12px
      width: 56px
      border-1px(7,17,27,0.1)
    .name
      padding-top: 2px 
      font-size: 14px
      color: rgb(7,17,27)
      line-height: 14px
    .desc, .extra
      margin-top: 8px
      font-size: 10px
      color: rgb(147,153,159)
      line-height: 10px
    .goodRate
      margin-left: 12px 
    .newPrice
      font-size: 14px
      color: red
      font-weight: 700
      line-height: 24px
</style>
