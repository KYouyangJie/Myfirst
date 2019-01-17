<template>
  <div id="add-blog" >
  <h2>添加博客</h2>
  <form v-if="!submited">
  	<label>博客标题：</label>
  	<input type="text" required v-model="blog.title"/>
  	<label>博客内容：</label>
  	<textarea  v-model="blog.content"></textarea>
  	<div id="checkboxes">
  		<label>主题：</label>
  		<label>Vue.js</label>
  		<input type="checkbox" value="Vue.js" v-model="blog.categories"/>
  		<label>angular.js</label>
  		<input type="checkbox" value="angular.js" v-model="blog.categories"/>
  		<label>Reaject.js</label>
  		<input type="checkbox" value="Reaject.js" v-model="blog.categories" />
  	</div>
  	<label>作者：</label>
  	<select v-model="blog.author">
  		<option v-for="author in authors">{{author}}</option>
  		
  	</select>
  	<button v-on:click.prevent="post">添加博客</button>
  </form>
  <p v-if="submited">博客添加成功</p>
  <div id="preview">
	<h3>博客总览</h3>
	<p>博客标题：{{blog.title}}</p>
	<p>博客内容：</p>
	<p>{{blog.content}}</p>
  	<p>博客分类:</p>
  	<p v-for="categorie in blog.categories">{{categorie}}</p>
  	<p>作者:{{blog.author}}</p>
  	
  	
  </div>
  </div>
</template>

<script>
	import axios from 'axios'
export default {
  name: 'add-blog',
  data () {
    return {
	blog:{
		title:"",
		content:"",
		categories:[],
		author:""
	},
	authors:["欧阳杰","谭沙","曹亚"],
	submited:false
	
    }
     
  },
  methods:{
  post:function(){
//	this.$http.post("https://wd3658003872umkxqv.wilddogio.com/posts.json",this.blog)
		axios.post("https://wd3658003872umkxqv.wilddogio.com/posts.json",this.blog)
  	.then((data)=>{
  		console.log(data);
  		this.submited=true;
  	})
  }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#add-blog *{
	box-sizing: border-box;
}
#add-blog{
	margin: 20px auto;
	max-width: 600px;
	padding: 20px;
}
label{
	display: block;
}
input[type='text'],textarea,select{
	display: block;
	width: 100%;
	padding: 8px;
}

#checkboxes label{
	display: inline-block;
	margin-top: 0px;
}
#checkboxes input{
	display: inline-block;
	margin-right: 10px;
}
button{
	display: block;
	margin-top: 20px;
	background: brown;
	color: wheat;
	padding: 16px;
	border-radius: 5px;
	font-size: 18px;
	cursor: pointer;
}
#preview{
	padding: 20px 20px;
	border: 1px dotted #ccc;
	margin: 30px 0;
}
h3{
	margin-top: 10px;
}
textarea{
	height: 200px;
}
</style>
