<template>
  <div class="body col-12">
    <div class="body-main col-10 p-0">

      <div class="body-main-content col-sm-6 pl-0" v-for="(item, i) in content">
        <div class="body-main-content-block block w-100 h-100">
          <div class="body-main-content-block-header w-100">
            <img class="body-main-content-block-header-img" :src=" i % 2 === 0 ? '1.png' : '2.png' ">
            <div class="body-main-content-block-header-title w-100 pb-0">{{item.title}}</div>
          </div>
        </div>
      </div>

    </div>
    <div class="body-side col-2 p-0">
      <div class="body-side-money block mb-4">
        <div class="body-side-money-title">Курс обмена валют:</div>
      </div>
      <div class="body-side-commercial mb-4 block" v-for="com in commercial">
        <div class="body-side-commercial-image w-100">
          <img class="body-side-commercial-image-img" :src="com.img">
          <div class="body-side-commercial-image-honor w-100"></div>
        </div>
        <div class="body-side-commercial-title w-100">{{com.title}}</div>
        
      </div>
      
    </div>
  </div>
</template>

<script>

export default {
  data(){
    return {
      content:[
        {
          title: 'Мои счета',
          img: '',
          about: ''
        },
        {
          title: 'Шаблоны операций',
          img: '',
          about: ''
        },
        {
          title: 'Мои счета',
          img: '',
          about: ''
        },
        {
          title: 'Шаблоны операций',
          img: '',
          about: ''
        },
        {
          title: 'Мои счета',
          img: '',
          about: ''
        },
        {
          title: 'Шаблоны операций',
          img: '',
          about: ''
        },
        {
          title: 'Мои счета',
          img: '',
          about: ''
        },
        {
          title: 'Шаблоны операций',
          img: '',
          about: ''
        },
      ],
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
  },

}
</script>

<style lang="scss" scoped>

  @import '@/assets/main.scss';

  .block{
    border: 1px solid $white;
    border-radius: 5px;
    box-shadow: 0.5px 1px 4px 0px rgba(0,0,0,0.25);
  }
  .body{
    &-main{
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: space-between;
      &-content{
        height: 365px;
        width: 470px;
        padding-bottom: 30px;
        padding-right: 30px;

        &-block{
          background-color: $grey_content;
          padding: 10px;

          &-header{
            display: flex;

            &-img{
              margin: -15px 15px 0 0;
              max-height: 59px;
            }
            &-title{
              color: $red_light;
              font-weight: bold;
              font-size: 1.5rem;
              border-bottom: 1px solid $red_hr;

            }
          }
        }
      }
    }
    &-side{
      
      &-money{
        background-color: #eaeaea;
        min-height: 170px;
        padding: 10px;

        &-title{
          font-size: 0.9rem;
          font-weight: bold;
          color: $grey_font;
        }
      }
      &-commercial{
        margin-botom: 15px;
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
    }
  }

</style>