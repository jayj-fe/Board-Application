<template>
  <div class="post-edit-page">
    <h1>게시물 수정</h1>
    <post-edit-form v-if="post"
      :post="post"
      @submit="onSubmit" />
    <p v-else>게시물을 불러오는 중 ...</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import api from '@/api'
import PostEditForm from '@/components/PostEditForm'

export default {
  name: 'PostEditPage',
  components: {
    PostEditForm
  },
  props: {
    postId: {
      type: String,
      required: true
    }
  },
  computed: {
    ...mapState([ 'post' ])
  },
  methods: {
    onSubmit (payload) {
      // console.log(payload)
      const { title, contents } = payload
      api.put(`/posts/${this.postId}`, { title, contents })
        .then(res => {
          this.$router.push({
            name: 'PostViewPage',
            params: { postId: res.data.id.toString() }
          })
        })
        .catch(err => {
          if (err.response.status === 401) {
            alert('로그인이 필요합니다.')
            this.$router.push({ name: 'Signin' })
          } else if (err.response.status === 403) {
            alert(err.response.data.msg)
            this.$router.back()
          } else {
            alert(err.response.data.msg)
          }
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
