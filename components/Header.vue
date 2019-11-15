<template>
  <div class="header col-12 ">
    <div class="header-ava col-1 p-0"></div>
    <div class="header-main col-11 h-100 pr-0">
      <div class="header-main-fio col-12 pr-0">
        My Account
      </div>
      <div class="header-main-sidebar col-12 pl-0 p-0" ref="sidebar">

        <img src="arrow.png" @click="(e)=>moveSidebar(e,true)">

        <div class="header-main-sidebar-item" v-for="(link, i) in links">

          <router-link class="header-main-sidebar-item-link overflow-hidden" :to="'/' + link.src" :key="'link-' + i" v-if="!link.pre_links">
            <div class="header-main-sidebar-item-link-title">{{link.title}}</div>
          </router-link>

          <div class="header-main-sidebar-item-link" :key="'link-' + i" v-else>
            <div class="header-main-sidebar-item-link-title">{{link.title}}</div>

            <div class="header-main-sidebar-item-link-drop_down">
              <div class="header-main-sidebar-item-link-drop_down-item" v-for="(down, j) in link.pre_links">
                <router-link class="header-main-sidebar-item-link-drop_down-item-link" :to="down.src" :key="'down-'+j" v-if="!down.pre_links">{{down.title}}</router-link>

                <div class="header-main-sidebar-item-link-drop_down-item-link" :key="'down-'+j" v-else>
                  {{down.title}}
                  <div class="header-main-sidebar-item-link-drop_down drop_right">
                    <div class="header-main-sidebar-item-link-drop_down-item" v-for="(right, k) in down.pre_links">
                      <router-link class="header-main-sidebar-item-link-drop_down-item-link" :to="right.src" :key="'right-'+k">{{right.title}}</router-link>
                    </div>
                  </div>
                </div>
                
              </div>
            </div>

          </div>

        </div>

        <img src="arrow.png" @click="(e)=>moveSidebar(e,false)">

      </div>
    </div>
  </div>
</template>

<script>
  export default{
    data(){
      return {
        links: [
          {
            title: 'Главная',
            src: ''
          },
          {
            title: 'Счета',
            src: ''
          },
          {
            title: 'Платежи',
            src: ''
          },
          {
            title: 'Переводы',
            pre_links: [
              {
                title: 'На свой счет внутри банка',
                src: ''
              },
              {
                title: 'На чужой счет внутри банка',
                pre_links: [
                  {
                    title: 'На свой счет внутри банка',
                    src: ''
                  },
                  {
                    title: 'На чужой счет внутри банка',
                    src: ''
                  },
                  {
                    title: 'В другой банк в национальной валюте',
                    src: ''
                  },
                  {
                    title: 'Межнародные платежи SWIFT',
                    src: ''
                  },
                ]
              },
              {
                title: 'В другой банк в национальной валюте',
                src: ''
              },
              {
                title: 'Межнародные платежи SWIFT',
                src: ''
              },
            ]
          },
          {
            title: 'Купля/продажа валюты',
            src: ''
          },
          {
            title: 'О нас',
            src: 'about_us'
          },
          {
            title: 'Наши контакты',
            src: 'contacts'
          }
        ]
      }
    },
    mounted(){

    },
    methods:{
      moveSidebar(e,left){
        let sidebar = this.$refs['sidebar'], move = 50
        sidebar.scrollTo({
            left: sidebar.scrollLeft + (move * (left ? -1 : 1)),
            behavior: "smooth"
        })
      }
    }
  }
</script>
<style lang="scss">

  @import '@/assets/main.scss';
  
  a{
    color: $grey_font;
    position: relative;
    overflow: hidden;

    &:hover{
      text-decoration: none;
    }
  }


  .header{
    height: 120px;
    padding-bottom: 25px;
    display: flex;
    z-index: 2;

    &-ava{
      background-color: $red;
      width: 95px;
      margin: 0;
    }
    &-main{
      display: flex;
      flex-wrap: wrap;
      &-fio{
        color: $red_light;
        font-weight: bold;
        font-size: 1.25rem;
        display: flex;
        &::before{
          content: "";
          margin: 0 0.5rem 0 0;
          height: 2rem;
          width: 2rem;
          background-color: $red;
          display: none;
        }
      }
      &-sidebar{
        position: relative;
        overflow-x: hidden;
        display: flex;
        height: 40px;
        border-radius: 5px;
        background-image: -moz-linear-gradient( 90deg, rgb( 203, 203, 203 ) 0%, rgb( 231, 231, 231 ) 100%);
        background-image: -webkit-linear-gradient( 90deg, rgb( 203, 203, 203 ) 0%, rgb( 231, 231, 231 ) 100%);
        box-shadow: 0.5px 0.866px 3px 0px rgba( 0, 0, 0 , 0.5 );

        &>img{
          display: none;
          z-index: 1;
          cursor: pointer;
          opacity: 0.6;
          position: sticky;
          right: 2px;
          height: 80%;
          top: 10%;

          &:first-child{
            transform: rotate(180deg);
            right: unset;
            left: 2px;
          }
        }
        &-item{
          padding: 0 25px;
          height: 100%;
          color: $grey_font;
          position: relative;

          &::after{
            content: "";
            border: 0.5px solid $grey_border;
            border-radius: 10px;
            position: absolute;
            top: 25%;
            height: 50%;
            right: 0;
          }


          &-link{
            cursor: pointer;
            white-space: nowrap;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100%;
            position: relative;

            &:hover{
              color: $grey_font;
              .header-main-sidebar-item-link-drop_down{
                display: block;
              }
            }

            &-title{

              &:hover{
                color: $grey_font;

                &::before{
                  content: "";
                  position: absolute;
                  width: 100%;
                  height: 100%;
                  bottom: -20px;
                  background: radial-gradient(ellipse at center, rgba(255,255,255,1) 0%,rgba(255,255,255,0) 70%);  
                }            
              }
            }
            &-drop_down{
              display: none;
              position: absolute;
              top: 40px;
              left: 0;
              background-color: $grey_side_bg;
              white-space: nowrap;

              &.drop_right{
                left: unset;
                top: 0;
                right: -100%;
                opacity: 0;
              }

              &-item{
                width: 100%;
                height: 2rem;
                display: flex;
                align-items: center;
                &-link{
                  position: relative;
                  display: flex;
                  align-items: center;
                  width: 100%;
                  padding: 0 10px;
                  height: 100%;

                  &:hover{
                    background-color: $white;
                    color: $red_light !important;

                    .header-main-sidebar-item-link-drop_down.drop_right{
                      opacity: 1;
                    }
                  }
                }
              }
            }

          }
        }
      }
    }

  }
@media screen and (max-width: 1070px){
  .header-main-sidebar>img{
    display: block;
  }
  .header-ava{
    display: none;
  }
  .header-main{
    flex: 0 0 100%;
    max-width: 100%;
  }
  .header-main-fio::before{
    display: block;
  }
}

</style>
