<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0" @click.stop="decreaseCart"></div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop="addCart"></div>
  </div>
</template>

<script>
import Vue from 'vue'
import {bus} from '../bus/bus'

export default {

  name: 'cartcontrol',

  props: {
    food: {
      type: Object
    }
  },

  methods: {
    addCart () {
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count++
      }
      bus.$emit('cart.add', event.target)
    },
    decreaseCart () {
      this.food.count--
    }
  }
}
</script>

<style lang="stylus">
.cartcontrol
  font-size 0
  .cart-decrease
    display inline-block
    padding 6px
    line-height 24px
    font-size 24px
    color rgb(0, 160, 220)
    &.move-enter-active, &.move-leave-active
      transition all .4s linear
    &.move-enter, &.move-leave-to
      opacity 0
      transform translate3d(24px, 0, 0) rotate(180deg)
    &.move-enter-to, &.move-leave
      opacity 1
      transform translate3d(0, 0, 0) rotate(0)
  .cart-count
    display inline-block
    vertical-align top
    width 12px
    padding-top 6px
    line-height 24px
    text-align center
    font-size 10px
    color rgb(147, 153, 159)
  .cart-add
    display inline-block
    padding 6px
    line-height 24px
    font-size 24px
    color rgb(0, 160, 220)
</style>

