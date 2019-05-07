<template>
  <div class="forum-list">
    <h2 class="list-title">
      <a href="#">{{ category.name }}</a>
      <router-link :to="{name: 'Category', params: {id: category['.key']}}"></router-link>
    </h2>

    <ForumList :forums="categoryForums" />
  </div>
</template>

<script>
import ForumList from './ForumList'
export default {
  components: {
    ForumList
  },

  props: {
    category: {
      required: true,
      type: Object
    }
  },

  computed: {
    categoryForums () {
      return Object.values(this.$store.state.forums)
        .filter(forum => forum.categoryId === this.category['.key'])
    }
  }
}
</script>