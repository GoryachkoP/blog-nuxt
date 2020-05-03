<template>
  <section class="admin-container">
    <h1>Welcome to adminpanel!</h1>
  </section>
</template>

<script>
export default {
  layout: 'admin',
  middleware: ['admin-auth']
}
</script>

