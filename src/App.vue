<template>
<div id="root">

<div v-show="show" class="joke-wrapper">
<img @click="show = !show" class="close_icon" :src="close_icon">	
<img class="trollFace" :src="trollFace">
<div class="content">
<h4 class="content-text">{{ daysJoke.content }}</h4>
</div>
<button @click='getJoke'>Joke!</button>
</div>


</div>
</template>

<script>
export default {
  name: 'App',
  data(){
  return {
  show: true,	
  close_icon: require('@/assets/close.png'),
  trollFace: require('@/assets/face.png'),
  daysJoke: {
      content:'Start your day with some jokes huh....'
      }
    }
  },
  methods:{
  updateJoke(data){
  this.daysJoke = data;
  },
  getJoke() {
  fetch("https://joke3.p.rapidapi.com/v1/joke/?rapidapi-key=b06e00e4edmshd0a33e810fcaab3p1534d2jsn1c271a11b7f6")
  .then(data => data.json())
  .then(result => this.updateJoke(result))
   }
  }	
 }

</script>

<style lang="scss">
@import '@/assets/colors.scss';
@import '@/assets/mixins.scss';
@import '@/assets/fonts.scss';

body {
	img,button {
		cursor: pointer;
	}
	display: flex;
	align-items: center;
	justify-content: center;
	text-align: center;
	background-color: $body-bgColor;
	font-family: $font;
	.joke-wrapper {
		padding-bottom: 30px;
		.trollFace {
		width: 100px;
		height: 100px;
		position: relative;
		z-index: 1;
		&:hover {
			transform: rotate(20deg);
			transition: .6s;
		}
	}
		margin-top: 25%;
		position:relativ;
		.close_icon{
			width:20px;
			height:20px;
			float: right;
			transform: translate(-10px,10px);
		}
		background-color: $wrapper-bgColor;
		width: 450px;
		height: 270px;
		box-shadow: 15px 15px 40px black;
	border-radius: 10px;
		button {
		transform: translate(0,-60px);
		border: none;
		width: 390px;
		height:40px;
		font-size: 20px;
		color: $text-color;
		font-family: $font;
		background-color: $button-bgColor;
		border-radius: 0 0 10px 10px;
		&:hover {
			background-color: $button-hover-color;
		}
	}
		.content {
			transform: translate(0,-60px);
			background-color: $content-bgColor;
			margin: 0 30px;
			color: $text-color;
			word-break: break-all;
			letter-spacing: 1px;
			word-spacing: 2px;
			font-size: 1.1rem;
			height:150px;
			@include border-radius;
			.content-text {
				padding: 30px 10px 10px 10px;
			}
	}
  }
}
</style>
