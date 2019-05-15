<template>
  <div class="col-large push-top">
    <h1>{{ thread.title }}</h1>
    <router-link
      :to="{name: 'ThreadEdit', params: {threadId: thread['.key']}}"
      class="btn-green btn-small"
      tag="button"
      >Edit</router-link>
    <p>
      By <a href="#" class="link-unstyled">{{user.name}}</a>, <AppDate :timestamp="thread.publishedAt" />.
      <span style="float:right; margin-top: 2px;" class="hide-mobile text-faded text-small">3 replies by 3 contributors</span>
    </p>
    <PostList :posts="posts"/>
    <PostEditor :threadId="id"/>
  </div>
</template>

<script>
import PostList from '@/components/PostList'
import PostEditor from '@/components/PostEditor'
export default {
  components: {
    PostList,
    PostEditor
  },
  props: {
    id: {
      required: true,
      type: String
    }
  },
  computed: {
    thread () {
      return this.$store.state.threads[this.id]
    },
    posts () {
      const postIds = Object.values(this.thread.posts)
      return Object.values(this.$store.state.posts)
        .filter(post => postIds.includes(post['.key']))
    },
    user () {
      return this.$store.state.users[this.thread.userId]
    }
  },

  methods: {
    addPost ({post}) {
      this.$store.dispatch('createPost', post)
    }
  }
}
</script>
