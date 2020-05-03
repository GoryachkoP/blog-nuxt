<template>
  <section class="admin-container">
    <h1>Welcome to adminpanel!</h1>
  </section>
</template>

<script>
export default {
  layout: 'admin',
  middleware: ['admin-auth'],
  mounted() {
    const { message } = this.$route.query
    if ( message === 'successLogin' ) {
      this.$message.success('Вы успешно вошли в систему!')
    }
  }
}
</script>

