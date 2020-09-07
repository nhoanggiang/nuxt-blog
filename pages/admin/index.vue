<template>
  <div class="admin-page">
    <section class="new-post">
      <AppButton @click="$router.push('/admin/new-post')"
        >Create Post</AppButton
      >
      <AppButton @click="onLogout">Logout</AppButton>
    </section>
    <section class="existing-posts">
      <h1>Existing Posts</h1>
    </section>
    <PostList is-admin :posts="loadedPosts" />
  </div>
</template>

<script>
// import PostList from '@/components/Posts/PostList'
// import AppButton from '@/components/UI/AppButton'
export default {
  // components: {
  //   PostList,
  //   AppButton,
  // },

  // layout: 'admin',

  middleware: ['check-auth', 'auth'],

  computed: {
    loadedPosts() {
      return this.$store.getters.loadedPosts
    },
  },

  methods: {
    onLogout() {
      this.$store.dispatch('logout')
      this.$router.push('/admin/auth')
    },
  },
}
</script>

<style scoped>
.admin-page {
  padding: 20px;
}

.new-post {
  text-align: center;
  border-bottom: 2px solid #ccc;
  padding-bottom: 10px;
}

.existing-posts h1 {
  text-align: center;
}
</style>
