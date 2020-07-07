<template>
	<div class="body">
		
    <div class="body-main col-12 p-0">

      <div class="body-main-content col-12 col-sm-12 col-md-6 col-lg-4 pl-0 pr-lg-4 pr-0 h-auto" v-for="(user, i) in users">
      	<div class="body-main-content-block block w-100 h-100">
          <div class="body-main-content-block-header w-100">
            <div class="body-main-content-block-header-title w-100 pb-1">
	            <img class="ava" :src="user.avatar ? user.avatar : 'default_avatar.png'">
		          {{user.name}}
		        </div>
          </div>
          <div class="body-main-content-block-body w-100">	          
	          <div class="body-main-content-block-body-content w-100">
	          	<div>E-mail:<span> {{user.email}}</span></div>
	          	<div>Телефон:<span> {{user.phone}}</span></div>
	          	<div>Сайт:<span> {{user.website}}</span></div>
	          	<div>Компания:<span> {{user.company.name}}</span></div>
	          	<div>Адрес:<span> {{user.address.city + " " + user.address.street + " " + user.address.suite}}</span></div>
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
				users: []
			}
		},
		created(){
			this.$axios.get('https://jsonplaceholder.typicode.com/users')
			.then(res => {
				this.users = res.data;
				console.log(this.users[0])
			})
			.catch(err => console.error(err))
		}
	}
</script>

<style lang="scss">
	@import '@/assets/scss/colors.scss';

	.ava{
		max-height: 2rem;
		min-height: 2rem;
		max-width: 2rem;
		min-width: 2rem;
		margin-right: 5px;
		border-radius: 50%;
	}
	.body-main-content-block-body{
		display: flex;
		height: 100%;
		align-items: flex-start;
		justify-content: flex-start;
		padding-top: 10px;

		&-content{

			&>div{
				display: flex;
				justify-content: space-between;
				height: auto;
				padding: 15px 0;
				color: $red;
				border-bottom: 1px solid $grey_border;
				&:last-child{
					border-bottom: none;
				}
				&>span{
					color: $grey_font;
					max-width: 70%;
			    overflow-wrap: break-word;
					text-align: right;
				}
			}
		}
	}
</style>