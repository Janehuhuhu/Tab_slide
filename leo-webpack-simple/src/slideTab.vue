<template>
	<div class='slide' :style='{width:(200*arr.length)+"px"}' @mouseover='over' @mouseout='out'>
		<div v-for='i in arr' :style='{backgroundImage:"url("+i+")",backgroundSize:"cover"}' :class='styles[$index]'></div>
	</div>
	
</template>

<script>
	export default{
		props:['slideData'],
		data:function(){
			return {
				needIndex:'',
				arr:[],
				styles:[],
				timer:''
			}
		},
		ready:function(){
			this.needIndex=this.slideData.index;
			this.arr=this.slideData.img;
			this.timer=this.slideData.timer;
			for(var i=0;i<this.arr.length;i++){
				this.styles.push("s"+i);
			};
			clearInterval(this.timer);
			this.timer=setInterval(()=>{
				this.styles.push(this.styles.shift());
			},10000000)
		},
		methods:{
			over:function(){
				clearInterval(this.timer);
			},
			out:function(){
				clearInterval(this.timer);
				this.timer=setInterval(()=>{
					this.styles.push(this.styles.shift());
				},1000)
			}
		}
	}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
.slide
{
	height:150px;	
}
.slide div
{
	width:200px;
	height:150px;
	position:absolute;
	top:250px;
	left:50%;
	margin-left:-75px;
	transition:0.3s;
	transform:perspective(800px);
}
.slide .s3
{
	opacity:1;
	z-index:5;
}
.slide .s2
{
	opacity:0.7;
	z-index:4;
	transform:perspective(800px) translateX(-100px) rotateY(30deg);
}
.slide .s1
{
	opacity:0.4;
	z-index:3;
	transform:perspective(800px) translateX(-200px) rotateY(60deg);
}
.slide .s0
{
	opacity:0;
	z-index:3;
	transform:perspective(800px) translateX(-300px) rotateY(90deg);
}
.slide .s4
{
	opacity:0.7;
	z-index:4;
	transform:perspective(800px) translateX(100px) rotateY(-30deg);
}
.slide .s5
{
	opacity:0.4;
	z-index:3;
	transform:perspective(800px) translateX(200px) rotateY(-60deg);
}
.slide .s6
{
	opacity:0;
	z-index:3;
	transform:perspective(800px) translateX(300px) rotateY(-90deg);
}
</style>
