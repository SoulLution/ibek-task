<template>
  <div class="body">
    <div class="body-main p-0">

      <div class="body-main-content col-sm-6 pl-0 pr-0 pb-4 pr-sm-4" v-for="(item, i) in content">
        <div class="body-main-content-block block w-100 h-100">
          <div class="body-main-content-block-header w-100">
            <img class="body-main-content-block-header-img" :src=" i % 2 === 0 ? '1.png' : '2.png' ">
            <div class="body-main-content-block-header-title w-100 pb-0">{{item.title}}</div>
          </div>
        </div>
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
    }
  },

}
</script>

<style lang="scss">

  @import '@/assets/scss/colors.scss';

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
        // width: 470px;
        // max-width: calc(100% - 12px);

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
  }

</style>