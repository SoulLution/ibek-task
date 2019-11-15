<template>
	<div class="body">
		<div class="contacts col-12">

			<yandex-map class="col-sm-6" :coords="mega" @click="onClick">
		    <ymap-marker :coords="mega" :icon="balloonTemplate" marker-id="1" hint-content="Мега парк"/>
		  </yandex-map>

		  <yandex-map class="col-sm-6" :coords="nurli" @click="onClick">
		    <ymap-marker marker-id="123" :coords="nurli" :icon="markerIcon"/>
		  </yandex-map>

		</div>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				mega: [43.264173, 76.929910],
				nurli: [43.230582, 76.945995],
				 balloonTemplate:{
		      layout: 'default',
				 	content: 'Мега Парк',
 		      contentOffset: [0, -25],
		      contentLayout: '<div class="baloon">$[properties.iconContent]</div>'
		    },
				markerIcon: {
		      layout: 'default#imageWithContent',
		      imageHref: 'arrow.png',
		      imageSize: [43, 43],
		      imageOffset: [0, 0],
		    }
			}
		},
	  computed: {
	   
	  },
		methods:{
			onClick(e) {
	      this.coords = e.get('coords');
	      console.log(this.coords)
	    }
		}
	}
</script>

<style lang="scss">
	@import '@/assets/main.scss';
	section{
		height: 400px;
	}
	.contacts{
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
	}
	.baloon{
		color: $red_light !important;
		font-weight: bold;
		z-index: 5;
		display: flex;
		justify-content: center;
		align-items: center;
		white-space: nowrap;
		padding: 0.5rem 4rem;
		background-color: $grey_bg;
		color: $grey_font;
		border: 1px solid $white;
		border-radius: 5px;
	}
</style>