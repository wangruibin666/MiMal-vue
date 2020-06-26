<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import storage from './storage/index'

export default {
  name: 'App',
  components: {

  },
  data() {
    return {

    }
  },
  mounted() {
    // storage.setItem('a', 1);
    // storage.setItem('user', {a:1});
    // storage.setItem('abc', {a:1}, 'user');
    // storage.clear('a');
    // storage.clear('a', 'user');
    this.getUser();
    this.getCartCount();
  },
  methods: {
    getUser() {
      this.axios.get('/user').then((res={})=> {
        this.$store.dispatch('saveUserName', res.username); 
      })
    },
    getCartCount() {
      this.axios.get('/carts/products/sum').then((res=0)=> {
        this.$store.dispatch('saveCartCount', res); 
      })
    }
  }
}
</script>

<style lang="scss">
@import './assets/scss/reset.scss';
@import './assets/scss/mixin.scss';
@import './assets/scss/modal.scss';
@import './assets/scss/config.scss';
@import './assets/scss/button.scss';
@import './assets/scss/base.scss';

</style>
