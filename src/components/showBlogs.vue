<template lang="html">
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>All Blog Articles</h1>
    <input type="text" v-model="keywords" placeholder="Search in Blogs">
    <div v-for="blog in blogsList" class="single-blog">
      <h2 v-rainbow>{{ blog.title | toUpperCase }}</h2>
      <article>{{ blog.body | snippet}}</article>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      blogs: [],
      keywords: ''
    }
  },
  methods: {

  },
  created() {
    this.$http.get("https://jsonplaceholder.typicode.com/posts").then(data => {
      this.blogs = data.body.slice(0, 10);
    });
  },

  computed: {
    blogsList: function(){
      return this.blogs.filter(blog => {
        return blog.title.match(this.keywords);
      });
    }
  },
  filters: {
    toUpperCase(value){
      return value.toUpperCase();
    }
  },
  directives: {
    'rainbow': {
      bind(el, binding, vnode){
        el.style.color = '#' + Math.random().toString().slice(2, 8);
      }
    }
  }
}
</script>

<style scoped lang="css">
#show-blogs{
  max-width: 800px;
  margin: 0 auto;
}

input[type='text'], textarea{
  display: block;
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}

.single-blog{
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}
</style>
