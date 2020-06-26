<template>
  <div class="order-header">
    <div class="w clearfix">
      <div class="header-logo">
        <a href="/#/index"></a>
      </div>
      <div class="title">
        <h2>{{title}}<slot name="tip"></slot></h2>
      </div>
      <div class="username">
        <a href="javascript:;">{{username}}</a>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'order-header',
  props: {
    title: String
  },
  computed:{
      username(){
        return this.$store.state.username;
      },
      cartCount(){
        return this.$store.state.cartCount;
      }
    }
}
</script>
<style lang="scss">
  .order-header {
    padding: 30px 0;
    .header-logo {
      float: left;
    }
    .title, .username {
      display: inline-block;
      height: 55px;
      line-height: 55px;
    }
    .title {
      float: left;
      color: #333;
      margin-left: 54px;
      h2 {
        font-size: 28px;
      }
      span {
        font-size: 14px;
        margin-left: 17px;
        color: #999;
        font-weight: bold;

      }
    }
    .username {
      float: right;
      a {
        color: #666;
        font-size: 16px;
      }
    }
  }
</style>