<template>
  <div class="forum-wrapper">
    <div class="col-full push-top">
      <div class="forum-header">
        <div class="forum-details">
          <h1>{{forum.name}}</h1>
          <p class="text-lead">{{forum.description}}</p>
        </div>
        <router-link
          class="btn-green btn-small"
          :to="{name: 'ThreadCreate', params: {forumId: this.forum['.key']}}">
          Start a thread
        </router-link>
      </div>
    </div>

    <div class="col-full">
      <div class="category-item">
        <div class="forum-list"></div>
      </div>
    </div>

    <div class="col-full push-top">
      <ThreadList :threads="threads"/>

      <div class="pagination">
        <button class="btn-circle" disabled>
          <i class="fa fa-angle-left"></i>
        </button>
        1 of 3
        <button class="btn-circle">
          <i class="fa fa-angle-right"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import ThreadList from '@/components/ThreadList'
export default {
  components: {
    ThreadList
  },

  props: {
    id: {
      required: true,
      type: String
    }
  },

  computed: {
    forum () {
      return this.$store.state.forums[this.id]
    },

    threads () {
      return Object.values(this.$store.state.threads)
        .filter(thread => thread.forumId === this.id)
    }
  }
}
</script>
<style>
@import "../assets/css/style.css";
.forum-wrapper {
  width: 100%;
}
</style>