<template>
  <v-list>
    test
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

export default {
  name: 'BBS',
  data: () => ({
    comments: []
  }),
  firestore() {
    // return {
    //   comments: db.collection('comments').orderBy('createdAt', 'desc')
    // }
    db.collection('comments')
      .get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          let data = {
            avater: doc.avater,
            content: doc.data().content,
            createdAt: doc.data().createdAt
          }
          this.comments.push(data)
        })
      })
      console.log('asdafsdfasdfasdfsad');
      
  }
}
</script>