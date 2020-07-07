<template>
  <div class="page">
    <div class="page-content d-flex px-2 flex-row flex-wrap">
      <Header />
      <nuxt class="col-12 col-md-10"/>
      <div class="body-side col-12 p-0 col-md-2 ">
        <div class="money block mb-4 mx-4 mx-md-0 mx-lg-0">
          <div class="money-title">Курс обмена валют:</div>
        </div>
        <div class="commercial col-12 d-none d-md-block" v-for="com in commercial">
          <div class="commercial-image w-100">
            <img class="commercial-image-img" :src="com.img">
            <div class="commercial-image-honor w-100"></div>
          </div>
          <div class="commercial-title w-100">{{com.title}}</div>
          
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import Header from '@/components/Header.vue'

  export default {
    components: { Header },
    data(){
      return{
        commercial: [
          {
            title: 'Кредит Auto',
            img: 'auto.png',
            src: '/'
          },
          {
            title: 'Депозиты',
            img: 'deposit.png',
            src: '/'
          }
        ]
      }
    }
  }
</script>

<style lang="scss">
@import '@/assets/scss/main.scss';

html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  overflow-x: hidden;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
  
.money{
  background-color: #eaeaea;
  min-height: 170px;
  padding: 10px;

  &-title{
    font-size: 0.9rem;
    font-weight: bold;
    color: $grey_font;
  }
}
.commercial{
  max-width: 100%;
  margin-bottom: 15px;
  cursor: pointer;
  z-index: 1;
  position: relative;

  &-image{
    width: 100%;

    &-img{
      width: 100%;
      height: 100%;
    }
    &-honor{
      height: 75%;
      background: linear-gradient(135deg, rgba(255,255,255,0.1) 0%, rgba(255,255,255,0.2) 50%, rgba(255,255,255,0) 51%);
      position: absolute;
      top: 0;
    }
  }
  &-title{
    background-color: $red_link;
    color: $white;
    padding: 10px;
    font-weight: bold;
    font-size: 0.9rem;
    z-index: 2;
  }
}

</style>
