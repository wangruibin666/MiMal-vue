<template>
  <div class="header">
    <div class="nav-topbar">
      <div class="w">
        <div class="nav-topbar-left">
          <a href="javascript:;">米出行</a>
          <a href="javascript:;">MUI</a>
          <a href="javascript:;">云服务</a>
          <a href="javascript:;">协议规则</a>
        </div>
        <div class="nav-topbar-user">
          <a href="javascript:;" v-if="username">{{username}}</a>
          <a href="javascript:;" v-if="!username" @click="login">登录</a>
          <a href="javascript:;" v-if="username">我的订单</a>
          <a href="javascript:;" class="my-cart" @click="goToCart"><span class="icon-cart"></span>购物车({{cartCount}})</a>
        </div>  
      </div>  
    </div>  
    <div class="nav-header">
      <div class="w">
        <div class="header-logo">
          <a href="#"></a>
        </div>
        <div class="header-menu">
          <div class="item-menu">
            <span>小米手机</span>
            <div class="children">
              <ul>
                <li class="product" v-for="(item, index) in phoneList" :key="index">
                  <a :href="'/#/product/'+item.id" target="_blank">
                    <div class="pro-img"><img v-lazy="item.mainImage" :alt="item.subtitle"></div>
                    <div class="pro-name">{{item.name}}</div>
                    <div class="pro-price">{{item.price | currency}}</div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
          <div class="item-menu">
            <span>RedMi手机</span>
            <div class="children">
              <ul>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="../../public/imgs/nav-img/nav-2.png" alt=""></div>
                    <div class="pro-name">红米9 pro</div>
                    <div class="pro-price">2999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="../../public/imgs/nav-img/nav-3.png" alt=""></div>
                    <div class="pro-name">红米9 pro</div>
                    <div class="pro-price">2999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="../../public/imgs/nav-img/nav-4.png" alt=""></div>
                    <div class="pro-name">红米9 pro</div>
                    <div class="pro-price">2999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="../../public/imgs/nav-img/nav-5.png" alt=""></div>
                    <div class="pro-name">红米9 pro</div>
                    <div class="pro-price">2999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="../../public/imgs/nav-img/nav-6.png" alt=""></div>
                    <div class="pro-name">红米9 pro</div>
                    <div class="pro-price">2999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img src="../../public/imgs/nav-img/nav-3-2.jpg" alt=""></div>
                    <div class="pro-name">红米9 pro</div>
                    <div class="pro-price">2999元</div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
          <div class="item-menu">
            <span>电视</span>
            <div class="children">
              <ul>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img v-lazy="'/imgs/nav-img/nav-3-1.jpg'" alt=""></div>
                    <div class="pro-name">mi TV</div>
                    <div class="pro-price">4999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img v-lazy="'/imgs/nav-img/nav-3-2.jpg'" alt=""></div>
                    <div class="pro-name">mi TV</div>
                    <div class="pro-price">4999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img v-lazy="'/imgs/nav-img/nav-3-3.png'" alt=""></div>
                    <div class="pro-name">mi TV</div>
                    <div class="pro-price">4999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img v-lazy="'/imgs/nav-img/nav-3-4.jpg'" alt=""></div>
                    <div class="pro-name">mi TV</div>
                    <div class="pro-price">4999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img v-lazy="'/imgs/nav-img/nav-3-5.jpg'" alt=""></div>
                    <div class="pro-name">mi TV</div>
                    <div class="pro-price">4999元</div>
                  </a>
                </li>
                <li class="product">
                  <a href="" target="_blank">
                    <div class="pro-img"><img v-lazy="'/imgs/nav-img/nav-3-6.png'" alt=""></div>
                    <div class="pro-name">mi TV</div>
                    <div class="pro-price">4999元</div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
        </div>
        <div class="header-search">
          <div class="wrapper">
            <input type="text" name="keyword">
            <a href="javascript:;"></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export  default{
    name: 'nav-header',
    data() {
      return {
        phoneList: []
      }
    },
    computed:{
      username(){
        return this.$store.state.username;
      },
      cartCount(){
        return this.$store.state.cartCount;
      }
    },
    filters: {
      currency(val) {
        if (!val) return '0.00';
        return '¥' + val.toFixed(2) + '元';
      }
    },
    mounted() {
      this.getProductList();
      
    },
    methods: {
      getProductList() {
        this.axios.get('./products', {
          params: {
            categoryId: '100012',
            // pageSize: 6
          }
        }).then((res)=> {
          if (res.list.length > 6) {
            this.phoneList = res.list.slice(0, 6);
          }
        })
      },
      goToCart() {
        this.$router.push('/cart');
      },
      login() {
        this.$router.push('/login');
      }
    }
  }
</script>
<style lang="scss">
@import '../assets/scss/base.scss';
@import '../assets/scss/mixin.scss';
@import '../assets/scss/config.scss';
  .header{
    .nav-topbar {
      height: 39px;
      line-height: 39px;
      background-color: #333333;
      color: #B0B0B0;
      .w {
        @include flex();
        a {
          display: inline-block;
          color: #B0B0B0;
          margin-left: 17px;
        }
        .my-cart {
          width: 110px;
          height: 39px;
          background-color: #FF6600;
          color: #fff;
          text-align: center;
          .icon-cart {
            @include bgImg(16px, 12px, '../../public/imgs/icon-cart-checked.png');
            margin-right: 4px;
          }
        }
      }
    }
    .nav-header {
      .w {
        position: relative;
        height: 112px;
        @include flex();
        
        .header-menu {
          // display: inline-block;
          width: 643px;
          padding-left: 209px;
          .item-menu {
            display: inline-block;
            color: #333;
            font-weight: bold;
            font-size: 16px;
            line-height: 112px;
            margin-right: 20px;
            span {
              cursor: pointer;
            }
            &:hover {
              color: $colorA;
              .children {
                height: 220px;
                opacity: 1;
              }
            }
            .children {
              position: absolute;
              height: 220px;
              top: 112px;
              left: 0;
              width: 1226px;
              height: 0;
              opacity: 0;
              background-color: #fff;
              overflow: hidden;
              border-top: 1px solid #E5E5E5;
              box-shadow: 0px 7px 6px 0px rgba(0, 0, 0, .11);
              z-index: 9;
              bottom: #fff;
              transition: all .5s;
              .product {
                float: left;
                width: 16.6%;
                height: 220px;
                font-size: 12px;
                line-height: 12px;
                text-align: center;
                a {
                  display: inline-block;

                }
                img {
                  width: auto;
                  height: 111px;
                  margin-top: 28px;
                }
                .pro-img {
                  height: 137px;
                }
                .pro-name {
                  font-weight: bold;
                  color: $colorB;
                  margin-bottom: 8px;
                  margin-top: 19px; 
                }
                .pro-price {
                  color: $colorA;

                }
                &::before {
                  content: ' ';
                  position: absolute;
                  top: 28px;
                  right: 0;
                  border-left: 1px solid $colorF;
                  height: 100px;
                  width: 1px;
                }
                &:last-child::before {
                  display: none;
                }  
              }
            }
          }
        }
        .header-search {
          width: 319px;
          .wrapper {
            height: 50px;
            border: 1px solid #E0E0E0;
            display: flex;
            align-items: center;
            input {
              border: none;
              border-right: 1px solid #E0E0E0;
              box-sizing: border-box;
              width: 264px;
              height: 50px;
              padding-left: 14px;
            }
            a {
              @include bgImg(18px, 18px, '../../public/imgs/icon-search.png');
              margin-left: 17px;
            }
          }
        }
      }
    }   
  }
</style>