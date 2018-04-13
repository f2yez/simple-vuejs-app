<template lang="html">
  <div id="add-blog">
    <h2>Add a new Blog Post</h2>
    <form v-if="!submitted">
      <label for="title">Title</label>
      <input type="text" required v-model.lazy="blog.title">
      <label for="content"></label>
      <textarea name="content" v-model.lazy='blog.content' rows="8" cols="80"></textarea>
      <div id="checkboxes">
        <label>News</label>
        <input type="checkbox" value="news" v-model="blog.categories">

        <label>Games</label>
        <input type="checkbox" value="games" v-model="blog.categories">

        <label>Articles</label>
        <input type="checkbox" value="article" v-model="blog.categories">

        <label>Videos</label>
        <input type="checkbox" value="videos" v-model="blog.categories">
      </div>
      <div id="author">
        <label>Author</label>
        <select v-model="blog.author">
          <option v-for="author in authors">{{ author }}</option>
        </select>
      </div>
      <br>
      <div>
        <button v-on:click.prevent="addNewBlog">Add Blog</button>
      </div>
    </form>
    <div v-if="submitted">
      <h3>Thanks for adding your post</h3>
    </div>
    <div id="preview">
      <h3>Preview Blog</h3>
      <p>Blog Title: {{ blog.title }}</p>
      <p>Blog Content:</p>
      <p>{{ blog.content }}</p>
      <p>Blog Categories:</p>
      <ul>
        <li v-for="category in blog.categories">{{ category }}</li>
      </ul>
      <p>Author: {{ blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      blog: {
        title: '',
        content: '',
        categories: []
      },
      authors:['Fayez', 'Dina', 'Sireen', 'Ahmed'],
      submitted: false
    }
  },
  methods: {
    addNewBlog: function(){
      this.$http.post('https://jsonplaceholder.typicode.com/posts', {
        title: this.blog.title,
        body: this.blog.content,
        userId: 1
      }).then(data => {
        console.log('response: ', data);
        this.submitted = true;
      });
    }
  }
}
</script>

<style scoped lang="css">
#add-blog *{
  box-sizing: border-box;
  border-radius: 5px;
}

#add-blog{
  margin: 20px auto;
  max-width: 500px;
}

label{
  display: block;
  margin: 20px 0 10px;
}scoped

input[type=checkbox] {
  width: 24px;
  height: 24px;
}
input[type=text], select, textarea {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}

h3{
  margin-top: 10px;
}

#checkboxes input{
  display: inline-block;
  margin-left: 10px;
}

#checkboxes label{
  display: inline-block;
}

button{
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #45a049;
}

</style>
