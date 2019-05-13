<template>
  <div class="post-list">
    <div class="post">
      <div class="user-info">
        <a href="#" class="user-name" v-bind="user.name">{{user.name}}</a>

        <a href="#">
          <img class="avatar-large" :src="user.avatar" alt>
        </a>

        <p class="desktop-only text-small">{{userPostsCount}} posts</p>

        <p class="desktop-only text-sthis.mall">23 threads</p>

        <span class="online desktop-only">online</span>
      </div>

      <div class="post-content">
        <template v-if="!editing">
          <div>{{post.text}}</div>
          <a @click.prevent="editing = true" href="#" style="margin-left: auto;" class="link-unstyled" title="Make a change">Edit<i class="fa fa-pencil"></i></a>
        </template>
        <div v-else><PostEditor :post="post" @save="editing = false" @cancel="editing = false" /></div>
      </div>

      <div class="post-date text-faded">
        <div v-if="post.edited" class="edition-info">edited</div>
        <AppDate :timestamp="post.publishedAt" />
      </div>
    </div>
  </div>
</template>
<script>
import {countObjectProperties} from '@/utils'
import PostEditor from './PostEditor'
export default {
  props: {
    post: {
      required: true,
      type: Object
    }
  },

  components: {
    PostEditor
  },

  data () {
    return {
      editing: false
    }
  },

  computed: {
    user () {
      return this.$store.state.users[this.post.userId]
    },

    userPostsCount () {
      return countObjectProperties(this.user.posts)
    }
  }
}
</script>
