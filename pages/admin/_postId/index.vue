<template>
  <div class="admin-post-page">
    <section class="update-form">
      <AdminPostForm :post="loadedPost" @submit="onSubmitted" />
    </section>
  </div>
</template>

<script>
// import axios from 'axios'
import AdminPostForm from '@/components/Admin/AdminPostForm'
export default {
  components: {
    AdminPostForm,
  },

  asyncData(context) {
    return context.app.$axios
      .$get('/posts/' + context.params.postId + '.json')
      .then((data) => {
        return {
          loadedPost: { ...data, id: context.params.postId },
        }
      })
      .catch((e) => context.error(e))
  },

  // data() {
  //   return {
  //     loadedPost: {
  //       author: 'Nguen Hoang Giang',
  //       title: 'My awesome Post',
  //       content: 'Cong hoa xa hoi chu nghia Viet Nam!',
  //       thumbnailLink:
  //         'https://res.cloudinary.com/people-matters/image/upload/q_auto,f_auto/v1578710070/1578710068.jpg',
  //     },
  //   }
  // },

  methods: {
    onSubmitted(editedPost) {
      this.$store.dispatch('editPost', editedPost).then(() => {
        this.$router.push('/admin')
      })
    },
  },

  layout: 'admin',

  middleware: ['check-auth', 'auth'],
}
</script>

<style scoped>
.update-form {
  width: 90%;
  margin: 20px auto;
}
@media (min-width: 768px) {
  .update-form {
    width: 500px;
  }
}
</style>
