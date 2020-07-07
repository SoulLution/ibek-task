<template>
	<div class="body">
		<div class="contacts col-12 px-0">

			<yandex-map class="col-12 col-md-9 mb-2 px-1" zoom="12" :coords="mega" @click="onClick">
		    <ymap-marker 
		    	:coords="mega" 
		    	:icon="balloonTemplate" 
		    	marker-id="1" 
		    	:balloon="{header: 'Mega Park Алматы'}"
		    />
		    <ymap-marker 
			    :coords="nurli" 
			    :icon="markerIcon" 
			    marker-id="123"
			  />
		  </yandex-map>

		  <!-- <yandex-map class="col-12 col-sm-6 mb-2 px-1" :coords="nurli" @click="onClick">
		    <ymap-marker 
			    :coords="nurli" 
			    :icon="markerIcon" 
			    marker-id="123"
			  />
		  </yandex-map> -->

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
				 	content: 'Мега парк',
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
	@import '@/assets/scss/colors.scss';
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