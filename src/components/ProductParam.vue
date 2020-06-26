<template>
  <div class="nav-bar" :class="{'is_fixed':isFixed}">
    <div class="w">
      <div class="pro-title">
        {{title}}
      </div>
      <div class="pro-param">
        <a href="javascript:;">概述</a><span>|</span>
        <a href="javascript:;">参数</a><span>|</span>
        <a href="javascript:;">用户评价</a>
        <slot name="buy"></slot>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'nav-bar',
  props: {
    title: String
  },
  data() {
    return {
      isFixed:false
    }
  },
  mounted() {
    window.addEventListener('scroll', this.initHeight)
  },
  methods: {
    initHeight() {
      let scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
      this.isFixed = scrollTop > 152? true:false;
    }
  },
  destroyed() {
    window.removeEventListener('scroll', this.initHeight,false);//false冒泡干掉initHeight事件
  }
}
</script>
<style lang="scss">
@import './../assets/scss/config.scss';
@import './../assets/scss/mixin.scss';
  .nav-bar {
    height: 70px;
    border-top: 1px solid #E5E5E5;
    background-color: #fff;
    line-height: 70px;
    z-index: 10;
    &.is_fixed{
      position: fixed;
      top: 0;
      box-shadow: 0 5px 5px #ccc;
      width: 100%;
    }
    .w {
      @include flex();
      .pro-title {
        font-size: 18px;
        color: #333;
        font-weight: bold;
      }
      .pro-param {
        font-size: 14px;
        a {
          color: #666;
        }
        span {
          margin: 0 10px;
        }
        .btn {
          margin-left: 10px;
        }
      }
    }
  }
</style>