<template>
  <div class="col-full push-top">
    <h1>
      Edit thread
      <i>{{thread.name}}</i>
    </h1>

    <ThreadEditor
      :title="thread.title"
      :content="text"
      @save="save"
      @cancel="cancel"
    />
  </div>
</template>

<script>
import ThreadEditor from '@/components/ThreadEditor'
export default {
  components: {
    ThreadEditor
  },
  props: {
    threadId: {
      required: true,
      type: String
    }
  },

  computed: {
    thread () {
      return this.$store.state.threads[this.threadId]
    },

    text () {
      return this.$store.state.posts[this.thread.firstPostId].text
    }
  },
  methods: {
    save ({title, text}) {
      this.$store.dispatch('updateThread', {
        id: this.threadId,
        title,
        text
      }).then(thread => this.$router.push({name: 'ThreadShow', params: {id: thread['.key']}}))
    },

    cancel () {
      this.$router.push({name: 'Forum', params: {id: this.forum['.key']}})
    }
  }
}
</script>

<style>
</style>
