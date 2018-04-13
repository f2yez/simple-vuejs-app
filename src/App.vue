<template>
  <div id="app">
    <header id="controls">
      <button @click="active_component = 'show-blogs'">Show All Blogs Articles</button>
      <button @click="active_component = 'add-blog'">Add New Blog Form</button>
    </header>
    <component v-bind:is="active_component"></component>
    <!-- <add-blog></add-blog> -->
    <!-- <show-blogs></show-blogs> -->
  </div>
</template>

<script>
import AddBlog from './components/addBlog.vue';
import ShowBlogs from './components/showBlogs.vue';
export default {
  name: 'app',
  components: {
    'add-blog': AddBlog,
    'show-blogs': ShowBlogs
  },
  data () {
    return {
      active_component: 'show-blogs'
    }
  }
}
</script>

<style scoped="">
header{
  box-sizing: border-box;
  margin: 0 auto;
  text-align: center;
}

#controls button{
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
#controls button:hover {
  background-color: #45a049;
}
</style>
