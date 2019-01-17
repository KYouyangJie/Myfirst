<template>
  <div id="Show-blog">
  	<div id="Show-blogs">
  <h1>博客总览</h1>
  <input type="text"placeholder="搜索" v-model="search" />
  <div class="single-blog" v-for="blog in fitereBlogs">
  	<router-link v-bind:to="'/blog/'+ blog.id">
  	<h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
  	</router-link>
  	<article>{{blog.content }}</article>
  
  </div>
  </div>
  <div id="pinglun">
  	<ul>
  		<h1>评论列表</h1>
  		<li v-for="pinglun in pinglunneiron">{{
  			pinglun
  		}} </li>
  	</ul>
  	<textarea v-model="pinglun"></textarea>
  	<button v-on:click.prevent="postpinglun">评论</button>
  </div>
  </div>
</template>

<script>
	import axios from 'axios'
export default {
  name: 'Show-blog',
  data () {
    return {
			blogs:[],
			search:"",
			pinglun:"",
			pinglunneiron:""
    }
  },
  created(){
//	this.$http.get("https://wd3658003872umkxqv.wilddogio.com/posts.json")
	axios.get("https://wd3375618231jbimnv.wilddogio.com/posts.json")
  	.then(function(data){
  		return data.data
  	}).then((data)=>{
  		this.pinglunneiron =data;
  	}),
		axios.get("https://wd3658003872umkxqv.wilddogio.com/posts.json")
  	
  	.then(function(data){
			return data.data;
  	}).then((data)=>{
  		var blogsArray =[];
  		for(let key in data){
  			data[key].id = key;
  			blogsArray.push(data[key]);
  		}
  		this.blogs = blogsArray;
  	})
  
  },
  computed:{
  	fitereBlogs:function(){
  		return this.blogs.filter((blog)=>{
  			return blog.title.match(this.search);
  		})
  	}
  },
  methods:{
  	postpinglun:function(){
  		axios.post("https://wd3375618231jbimnv.wilddogio.com/posts.json",this.pinglun)
  		.then((data)=>{
  			console.log(data);
  			this.pinglun="";
  			window.location.reload();
  		})
  	},
  	
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#Show-blogs{
	max-width: 900px;
	margin: 0 auto;
	background: darkkhaki;
	padding: 20px;
}
#Show-blogs input{
	width: 100%;
	line-height: 30px;
}
h1{
	text-align: center;
}
.single-blog{
	padding: 30px;
	margin: 20px 20px;
	box-sizing: border-box;
	background: #eee;
	margin-bottom: 20px;
}
#pinglun{
	max-width: 900px;
	margin: 0 auto;
	margin-bottom: 100px;
}
textarea{
	width: 100%;
	margin-top: 20px;
	margin-bottom: 20px;
	height: 150px;
	
}
#pinglun button{
	background: darkcyan;
	padding: 10px;
	border-radius: 5px;
	font-size: 18px;
	float: right;
}
</style>
