<template>
  <article class="post">
    <header class="post__header">
      <div class="post__title">
        <h1>Post title</h1>
        <nuxt-link to='/'>
          <i class="el-icon-back"></i>
        </nuxt-link>
      </div>
      <div class="post__info">
        <small>
          <i class="el-icon-date"></i>
          {{ new Date().toLocaleString() }}
        </small>
        <small>
          <i class="el-icon-view"></i>
          42
        </small>
      </div>
      <div class="post__image">
        <img 
          src="https://cdn.flixbus.de/2017-09/kiev-header.jpg"
          alt="post image"
          class="post-image"
        >
      </div>
    </header>
    <main class="post__content">
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. 
        Eos aut veniam magni dignissimos non adipisci sequi 
        perspiciatis, eius nostrum commodi!</p>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. 
        Eos aut veniam magni dignissimos non adipisci sequi 
        perspiciatis, eius nostrum commodi!</p>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. 
        Eos aut veniam magni dignissimos non adipisci sequi 
        perspiciatis, eius nostrum commodi!</p>
    </main>

    <footer>
      <!-- Form -->

      <div class="comments" v-if="true">
        <app-comment
          v-for="comment in 4"
          :key="comment"
          :comment="comment"
        />
      </div>
      <div class="text-center" v-else>Коментариев нет!</div>
    </footer>
  </article>
</template>

<script>
import AppComment from '@/components/main/Comment.vue'
  export default {
    components: {
      AppComment
    },
    validate({ params }) {
      return Boolean(params.id)
    }
  }
</script>

<style lang="scss" scoped>
  .post {
    max-width: 600px;
    margin: 0 auto;

    .post__title {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1rem;
    }

    .post__info {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: .5rem;
    }

    .post__image {
      img {
        width: 100%;
        height: auto;
      }
    }

    .post__header {
      margin-bottom: 1.5rem;
    }

    .post__content {
      margin-bottom: 2rem;
    }
  }
</style>
