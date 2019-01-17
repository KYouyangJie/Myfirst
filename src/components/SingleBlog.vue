<template>
	<div id="single-blog">
		<h1>{{blog.title}}</h1>
		<article>{{blog.content}}</article>
		<p>作者：{{blog.author}}</p>
		<button v-on:click="deleteSingleBlog()">删除</button>
	</div>
</template>

<script>
	import axios from 'axios'
	export default{
	name:"single-blog",
	data(){
		return{
			id:this.$route.params.id,
			blog:{}
		}
	
	},
		created(){
//			this.$http.get('https://wd3658003872umkxqv.wilddogio.com/posts/'+this.id+
//			".json"
//			)
		axios.get('https://wd3658003872umkxqv.wilddogio.com/posts/'+this.id+
			".json")
			.then((data)=>{
				this.blog = data.data
			})
		},
		methods:{
		deleteSingleBlog(){
			this.$http.delete('https://wd3658003872umkxqv.wilddogio.com/posts/'+this.id+
			".json").then(function(){
				 this.$router.push({path:'/'})
			})
		}
		}
}
</script>

<style>
	#single-blog{
		max-width: 960px;
		margin: 0 auto;
		padding: 20px;
		background: #EEEEEE;
		border: 1px dotted #aaa;
	}
</style>