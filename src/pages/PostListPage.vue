<template>
  <div class="post-list-page">
    <h1>포스트 게시글</h1>
    <post-list :posts="posts" />
    <router-link :to="{ name: 'PostCreatePage' }">글쓰기</router-link>
  </div>
</template>

<script>
import PostList from '../components/PostList'
import { mapState, mapActions } from 'vuex'

export default {
  name: 'PostListPage',
  components: {
    PostList
  },
  created () {
    this.fetchPostList()
  },
  computed: {
    ...mapState([ 'posts' ])
  },
  methods: {
    ...mapActions(['fetchPostList'])
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
