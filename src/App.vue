<template>
  <div id="app">
 <!--  <add-blog> </add-blog>-->
 <!--<Show-blog></Show-blog>-->
 <blog-header></blog-header>

<router-view></router-view>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import AddBlog from './components/AddBlog'
import ShowBlog from './components/ShowBlog'
import BlogHeader from './components/BlogHearder'
import SingleBlog from './components/SingleBlog'

export default {
  name: 'App',
  components: {
    HelloWorld,AddBlog,ShowBlog,BlogHeader,SingleBlog
  }
}
</script>

<style>

</style>
