<template>
  <div class="empty-layout">
    <div class="empty-layout__login">
      <nuxt />
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    error() {
      return this.$store.getters.getError
    }
  },
  watch: {
    error(value) {
      this.$message.error(value)
    }
  }
}
</script>


<style lang="scss" scoped>
  .empty-layout {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100vh;
  }
</style>

