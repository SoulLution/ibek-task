<template>
	<div class="body col-12">
		
    <div class="body-main col-12 p-0">

      <div class="body-main-content col-sm-4 pl-0" v-for="(user, i) in users">
      	<div class="body-main-content-block block w-100 h-100">
          <div class="body-main-content-block-header w-100">
            <div class="body-main-content-block-header-title w-100 pb-0">{{user.name}}</div>
          </div>
          <div class="body-main-content-block-body w-100">
	          <img class="body-main-content-block-body-ava" :src="user.avatar ? user.avatar : 'default_avatar.png'">
	          <div class="body-main-content-block-body-content w-100">
	          	<div>E-mail: {{user.email}}</div>
	          	<div>Телефон: {{user.phone}}</div>
	          	<div>Сайт: {{user.website}}</div>
	          	<div>Компания: {{user.company.name}}</div>
	          	<div>Адресс: {{user.address.city + " " + user.address.street + " " + user.address.suite}}</div>
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
	@import '@/assets/main.scss';

	.body-main-content-block-body{
		display: flex;
		height: 100%;
		align-items: flex-start;
		justify-content: flex-start;
		padding-top: 10px;

		&-ava{
			height: auto;
			width: 30%;
			margin-right: 5px;
			border-radius: 50%;
			border: 1px solid $white;
		}
		&-content{

			&>div{
				border-bottom: 1px solid $grey_border;
			}
		}
	}
</style>