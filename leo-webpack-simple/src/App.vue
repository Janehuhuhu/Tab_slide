<template>
	<div id='app'>
		<Tab :all-data='tabNode'></Tab>
		<Slide :slide-data='slideNode'></Slide>
	</div>
</template>

<script>
	import Tab from './tab.vue'
	import Slide from './slideTab.vue'
	export default{
		data:function(){
			return {
				tabNode:{
					img:['./src/img/1.jpg','./src/img/2.jpeg','./src/img/3.jpg','./src/img/4.jpg','./src/img/5.jpg','./src/img/6.jpeg','./src/img/7.jpeg'],
					index:0,
					timer:null,
					bottomNode:-55,
					leftNode:-75
				},
				slideNode:{
					img:['./src/img/1.jpg','./src/img/2.jpeg','./src/img/3.jpg','./src/img/4.jpg','./src/img/5.jpg','./src/img/6.jpeg','./src/img/7.jpeg'],
					index:0,
					timer:null
				}
			}			
		},
		components:{Tab,Slide}
	}
	
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
</style>
