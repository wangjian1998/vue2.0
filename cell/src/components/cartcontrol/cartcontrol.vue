<template>
  <div class="cartcontrol">
    <transition name="decrease">
    <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0" @click="decreaseCart"></div>
    </transition>
    <!-- <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0" @click="decreaseCart"></div> -->
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script  type="text/ecmascript-6">
import Vue from 'vue'
export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    addCart(event){
      if(!event._constructed){
        return;
      }
      if(!this.food.count){
        Vue.set(this.food,'count',1)
      }else{
        this.food.count++
      }
      this.$emit('cart.add',event.target);
    },
    decreaseCart(){
       if(!event._constructed){
        return;
      }
      if(this.food.count){
        this.food.count--;
      }
    }
  },
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
.cartcontrol {
  font-size: 0;

  .decrease.enter,.decrease-leave-to{
     opacity: 0;
     transform: translate3d(12px,0,0);
  }
  .decrease-enter-active,.decrease-leave-active{
     transition: all 0.4s linear;
    
  }
  .cart-decrease {
    display: inline-block;
    font-size: 24px;
    line-height: 24px;
  }

  .cart-count {
    display: inline-block;
    line-height :24px;
    vertical-align :top;
    width:12px;
    font-size:12px;
    text-align: center;
    color:rgb(147,153,159);
  }

  .cart-add {
    display: inline-block;
    font-size: 24px;
    line-height: 24px;
    color:rgb(0,160,220);
  }
}
</style>