<template>
  <v-list>
    essdfsdfasdasdasdas
    <template v-for="(comment, index) in comments">
      <v-list-tile :key="index" avatar>
        <v-list-tile-avatar>
          <img :src="comment.avatar" />
        </v-list-tile-avatar>

        <v-list-tile-content>
          <v-list-tile-sub-title class="text--primary subheading">{{comment.content}}</v-list-tile-sub-title>
          <v-list-tile-sub-title>{{comment.createdAt.toDate().toLocaleString()}}</v-list-tile-sub-title>
        </v-list-tile-content>

        <v-list-tile-action></v-list-tile-action>
      </v-list-tile>
      <v-divider :key="comment.id"></v-divider>
    </template>
  </v-list>
</template>

<script>
import { db } from '~/plugins/firebase.js'

console.log(
  process.env.FB_API_KEY,
  process.env.FB_AUTH_DOMAIN,
  process.env.FB_DATABASE_URL,
  process.env.FB_PROJECTID,
  process.env.FB_STORAGE_BUCKET,
  process.env.FB_MESSAGING_SENDER_ID
)

export default {
  name: 'BBS',
  data: () => ({
    comments: []
  }),
  firestore() {
    return {
      comments: db.collection('comments').orderBy('createdAt', 'desc')
      // comments: db.collection('comments').doc('uBqkISFQ0F191cgGOsy1').orderBy('createdAt', 'desc')
    }
  }
}
</script>