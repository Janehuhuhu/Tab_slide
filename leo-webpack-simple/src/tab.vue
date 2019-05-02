<template>
	<div id='outer'  @mouseover='over' @mouseout='out'>
		<div v-for='i in arr' :style='{backgroundImage:"url("+i+")",backgroundSize:"cover"}' v-show='$index==needIndex?true:false' transition='leo'></div>
		<ul class='selectNode' :style='{width:arr.length*14+"px"}'>
			<li v-for='i in arr' :class='$index==needIndex?"active":""' @click='needIndex=$index'></li>
		</ul>
		<ul class='imgNode' :style='{width:arr.length*75+"px",bottom:bottomN+"px",left:leftN+"px"}'>
			<li v-for='i in arr' :style='{backgroundImage:"url("+i+")",backgroundSize:"cover"}' :class='$index==needIndex?"active":""'></li>
		</ul>
	</div>
	
</template>

<script>
	export default{
		props:['allData'],
		data:function(){
			return {
				arr:[],
				needIndex:'',
				timer:'',
				bottomN:'',
				leftN:'',
			}
		},
		ready:function(){
			this.arr=this.allData.img;
			this.needIndex=this.allData.index;
			this.timer=this.allData.timer;
			this.bottomN=this.allData.bottomNode;
			
			clearInterval(this.timer);
			this.timer=setInterval(()=>{
				if(this.needIndex==this.arr.length-1||this.needIndex==0){
					this.leftN=0;
				}
				else if(this.needIndex<4)
				{
					this.leftN=this.allData.leftNode*this.needIndex;
				}
				this.needIndex++;
				this.needIndex==this.arr.length&&(this.needIndex=0);
				
			},1000);
			
		},
		methods:{
			over:function(){
				this.bottomN=0;
				clearInterval(this.timer);
			},
			out:function(){
				clearInterval(this.timer);
				if(this.needIndex==0){
					this.leftN=0;
				}
				else if(this.needIndex<4)
				{
					this.leftN=this.allData.leftNode*this.needIndex;
				}
				this.bottomN=-55;
				this.timer=setInterval(()=>{
				this.needIndex++;
				this.needIndex==this.arr.length&&(this.needIndex=0);
				},1000)
			}
		}
	
	}
	
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
  background:#ccc;
}
*{margin:0;padding:0;list-style:none;}
#outer
{
	width:300px;
	height:200px;
	position:absolute;
	left:50%;
	transform:translateX(-50%);
	overflow:hidden;
}
#outer div
{
	width:100%;
	height:100%;
	position:absolute;
	
}
.selectNode
{
	position:absolute;
	bottom:15px;
	left:50%;
	transform:translateX(-50%);
	height:12px;
	background:rgba(255,255,255,0.3);
	z-index:10;
}
.selectNode li
{
	width:8px;
	height:8px;
	border-radius:50%;
	background:rgba(255,255,255,0.5);
	margin:2px 3px;
	float:left;
}
.selectNode li.active
{
	background:red;
}
.imgNode
{
	height:55px;
	position:absolute;
	z-index:11;
	background:rgba(255,255,255,0.8);
	
}
.imgNode li
{
	width:70px;
	height:50px;
	margin:2.5px;
	float:left;
	opacity:0.5;
}
.imgNode li.active
{
	opacity:1;
}
.leo-transition
{
	transition:0.5s;
	opacity:1;
}
.leo-enter
{
	opacity:0;
}
.leo-leave
{
	opacity:0;
}

</style>
