<template>
  <div id="app">
      <div class="input-form">
          <b-icon-search class="icon"></b-icon-search>
          <b-input v-model="searchText" class="input" placeholder="Filter by author..." type="text"></b-input>
      </div>
      <b-container class="card-columns">
          <post-card v-for="post in filteredPosts" :key="post.id" :post="post"></post-card>
      </b-container>
  </div>
</template>

<script>
import {fetchAuthors, fetchPosts} from "@/api";
import PostCard from "@/components/PostCard.vue";

export default {
    name: 'App',
    components: {PostCard},
    data() {
        return {
            posts: [],
            authors: [],
            searchText: ""
        }
    },
    async created() {
        await this.getPosts()
    },
    methods: {
        async getPosts() {
            const response = await fetchPosts()
            this.authors = await fetchAuthors()
            this.posts = response.map(post => ({...post, author: this.authors[post.userId - 1]}))
        },
    },
    computed: {
        filteredPosts() {
            if (this.searchText) {
                return this.posts.filter(post => {
                    return post.author.name.toLowerCase().includes(this.searchText.toLowerCase())
                })
            }
            return this.posts
        }
    }
}
</script>

<style lang="scss">
#app {
    background: #e5f2ff;
}
.input-form {
    display: flex;
    max-width: 440px;
    padding: 12px;
    margin: auto;
    .icon {
        align-self: center;
        margin: 10px;
    }
}

.card-columns {
    column-count: 3;
}
@media screen and (max-width:1440px) {
    .card-columns {
        column-count: 2;
    }
}
@media screen and (max-width:768px) {
    .card-columns {
        column-count: 1;
    }
}
</style>
