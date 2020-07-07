<template>
  <div class="header col-12 ">
    <div class="header-ava col-1 p-0"></div>
    <div class="header-main col-11 h-100 pr-0">
      <div class="header-main-fio col-12 pr-0">
        My Account
        <div class="burger" :class="{'active': sidebar}" @click="sidebar = !sidebar"><div></div></div>
      </div>
      <div class="sidebar col-12 pl-0 p-0" :class="{'active': sidebar}" ref="sidebar">

        <div class="d-flex justify-content-end p-4">
          <div class="burger active" @click="sidebar = false"><div></div></div>
        </div>

        <div class="sidebar-item" v-for="(link, i) in links">

          <router-link class="sidebar-item-link overflow-hidden" :to="'/' + link.src" :key="'link-' + i" v-if="!link.pre_links">
            <div class="sidebar-item-link-title">{{link.title}}</div>
          </router-link>

          <div class="sidebar-item-link" :key="'link-' + i" v-else>
            <div class="sidebar-item-link-title more" @click="checkOpen('first-' + i)">{{link.title}}</div>

            <div class="drop_down" :class="{'active' : open.find(x => x === 'first-' + i)}">
              <div class="drop_down-body">
                <div class="drop_down-item" v-for="(down, j) in link.pre_links">
                  <router-link class="drop_down-item-link" :to="down.src" :key="'down-'+j" v-if="!down.pre_links">{{down.title}}</router-link>

                  <div class="drop_down-item-link more" @click="checkOpen('second-' + i)" :key="'down-'+j" v-else>
                    <span>{{down.title}}</span>
                    <div class="drop_down drop_right" :class="{'active' : open.find(x => x === 'second-' + i)}">
                      <div class="drop_down-body">
                        <div class="drop_down-item" v-for="(right, k) in down.pre_links">
                          <router-link class="drop_down-item-link" :to="right.src" :key="'right-'+k">{{right.title}}</router-link>
                        </div>
                      </div>
                    </div>
                  </div>
                  
                </div>
              </div>
            </div>

          </div>

        </div>


      </div>
    </div>
  </div>
</template>

<script>
  export default{
    data(){
      return {
        sidebar: false,
        open: [],
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
    watch:{
       $route(to, from) {
        this.sidebar = false
      }
    },
    methods:{
      checkOpen(index){
        // let find = this.open.find((x, i) => x === index ? i : false)
        let find = this.open.indexOf(index)
        console.log(find)
        if(find > -1)
          this.open.splice(find, 1)
        else
          this.open.push(index)
      }
    }
  }
</script>
<style lang="scss" scoped>
  @import '@/assets/scss/colors.scss';
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
    overflow: visible;
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
        align-items: center;
        &::before{
          content: "";
          margin: 0 0.5rem 0 0;
          height: 2rem;
          width: 2rem;
          background-color: $red;
          display: none;
        }
      }
    }
  }
  .sidebar{
    position: relative;
    display: flex;
    height: 40px;
    border-radius: 5px;
    background-image: -moz-linear-gradient( 90deg, rgb( 203, 203, 203 ) 0%, rgb( 231, 231, 231 ) 100%);
    background-image: -webkit-linear-gradient( 90deg, rgb( 203, 203, 203 ) 0%, rgb( 231, 231, 231 ) 100%);
    box-shadow: 0.5px 0.866px 3px 0px rgba( 0, 0, 0 , 0.5 );

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
          .drop_down{
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

      }
    }
  }
  .drop_down{
    display: none;
    position: absolute;
    top: 15px;
    left: -50px;
    border-radius: 5px;
    padding: 25px;
    white-space: nowrap;
    &-body{
      border: 1px solid $white;
      background-color: $grey_side_bg;
    }

    &.drop_right{
      left: unset;
      top: -25px;
      right: calc(-100% - 25px);
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

          .drop_down.drop_right{
            opacity: 1;
          }
        }
      }
    }
  }
  .burger{
    margin-left: 1rem;
    height: 1rem;
    width: 24px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
    display: none;
    &>div, &:after, &:before{
      content: "";
      width: 100%;
      height: 1px;
      background-color: $grey_border;
      transition: 0.3s;
    }
    &.active{
      &:before{
        transform: rotate(45deg) translate(5px, 6px);
      }
      &:after{
        transform: rotate(-45deg) translate(5px, -6px);
      }
      &>div{
        opacity: 0;
      }
    }
  }
@media screen and (max-width: 1070px){
  .burger{
    display: flex;
  }
  .sidebar{
    position: fixed;
    flex-direction: column;
    height: 100vh;
    max-width: 425px;
    left: -425px;
    top: 0;
    transition: 0.3s;
    &.active{
    left: 0;

    }
    &-item{
      height: auto;
      padding: 0;
      &:after{
        display: none;
      }
      &-link{
        padding: 1rem 25px;
        flex-direction: column;
        align-items: flex-start;
        background-color: unset;
        &-title::before{
          display: none;
        }
        & .more{
          width: 100%;
          &:after{
            content: "";
            margin-top: 4px;
            margin-right: -4px;
            right: 12px;
            position: absolute;
            max-height: 12px;
            min-height: 12px;
            max-width: 12px;
            min-width: 12px;
            transform: rotate(45deg);
            border-bottom: 1px solid $grey_border;
            border-right: 1px solid $grey_border;
          }
        }
      }
    }
  }
  .drop_down, .drop_down.drop_right{
    position: relative;
    width: 100%;
    left: unset;
    right: unset;
    padding: 0;
    height: 100%;
    max-height: 0;
    opacity: 1;
    display: block;
    overflow: hidden;
    border-radius: 0;
    border-left: 1px solid $grey_border;
    transition: 0.3s;
    &-item{
      height: auto;
      &-link{
        align-items: flex-start;
        text-align: left;
        flex-direction: column;
        white-space: pre-wrap;
        background-color: unset !important;
      }
    }
    &.active{
      max-height: 50vh;
    }
    &-body{
      border: none;
      background-color: transparent;
    }

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
