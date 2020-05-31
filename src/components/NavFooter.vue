<template>
  <div class="footer">
    <div class="footer-logo">
      <img src="/imgs/logo-footer.png" alt="">
      <p>小米商城</p>
    </div>
    <div class="footer-link">
      <a href="" target="_blank">河畔一脚主页</a><span>|</span>
      <a href="">vue全栈课程</a><span>|</span>
      <a href="">react全家桶</a><span>|</span>
      <a href="">微信支付</a>
    </div>
    <div class="copyright">@@@@@@@@@@@@@<span class="domain">xiaomi</span>@@@@@@@@@@@@@</div>
  </div>
</template>
<script>
  export  default{
    name: 'nav-footer'
  }
</script>
<style lang="scss">
  .footer {
    height: 234px;
    border-top: 4px solid #FF6600;
    background-color: #333333;
    color: #999999;
    font-size: 16px;
    text-align: center;
    .footer-logo {
      margin-top: 45px;
      margin-bottom: 31px;
      img {
        height: 36px;
        width: 53px;
        margin-bottom: 13px;
      }
    }
    .footer-link {
      a {
        color: #999999;
        display: inline-block;

      }
      span {
        margin: 0 10px;
      }
      margin-bottom: 13px;
    }
    .copyright {
      .domain {
        color: #FF6600;
      }
    }
  }
</style>