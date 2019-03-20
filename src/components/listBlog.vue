<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h1>List Blog Titles</h1>
    <input type="text" v-model="search" placeholder="Search Blogs">
    <div class="single-blog" v-for="blog in filteredBlogs">
      <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
    </div>
  </div>
</template>

<script>
import searchMixin from "../mixins/searchMixin";
export default {
  data() {
    return {
      blogs: [],
      search: []
    };
  },
  methods: {},
  created() {
    this.$http
      .get("https://jsonplaceholder.typicode.com/posts")
      .then(function(data) {
        this.blogs = data.body.slice(0, 10);
      });
  },
  computed: {},

  //Local Filters
  filters: {
    "to-uppercase": function(value) {
      return value.toUpperCase();
    }
  },
  //   directives: {
  //     rainbow: {
  //       bind(el, binding, vnode) {
  //         el.style.color =
  //           "#" +
  //           Math.random()
  //             .toString()
  //             .slic(0, 8);
  //       }
  //     }
  //   }
  mixins: [searchMixin]
};
</script>

<style>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  box-sizing: border-box;
  margin: 20px 0;
  background: #eee;
}
</style>
