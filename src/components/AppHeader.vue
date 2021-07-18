<template>
  <div class="app-header">
    <h1>Community</h1>
    <div v-if="isAuthorized">
      <strong>
        <button type="button" @click='toggle'>{{me.name}}님 환영합니다</button>
        <i v-if="!isActive" class="fas fa-sort-down"></i>
        <i v-else class="fas fa-sort-up"></i>
      </strong>
      <ul v-if="isActive">
        <li><button type="button" @click='onClickSignout'>로그아웃</button></li>
      </ul>
    </div>
    <div v-else>
      <router-link :to="{ name: 'Signin' }">로그인</router-link>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapState, mapActions } from 'vuex'
export default {
  name: 'AppHeader',
  computed: {
    ...mapGetters([ 'isAuthorized' ]),
    ...mapState([ 'me' ])
  },
  data () {
    return {
      isActive: false
    }
  },
  methods: {
    toggle () {
      this.isActive = !this.isActive
    },
    onClickSignout () {
      this.signout()

      if (this.$route.name !== 'PostListPage') {
        this.$router.push({ name: 'PostListPage' })
      }
    },
    ...mapActions([ 'signout' ])
  }
}
</script>

<style scoped>
  button{
    background:none
  }
</style>
