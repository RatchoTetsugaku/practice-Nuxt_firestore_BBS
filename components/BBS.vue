<template>
  <v-list three-line>
    <template v-for="(message, index) in messages">
      <v-list-tile :key="index" avatar>
        <v-list-tile-avatar>
          <img :src="message.avatar" />
        </v-list-tile-avatar>

        <v-list-tile-content>
          <v-list-tile-sub-title class="text--primary subheading">{{message.content}}</v-list-tile-sub-title>
          <v-list-tile-sub-title>{{message.createdAt.toDate().toLocaleString()}}</v-list-tile-sub-title>
        </v-list-tile-content>

        <v-list-tile-action></v-list-tile-action>
      </v-list-tile>
      <v-divider :key="message.id"></v-divider>
    </template>
  </v-list>
</template>

<script>
import { db } from '~/plugins/firebase.js'

export default {
  name: 'BBS',
  data: () => ({
    messages: []
  }),
  firestore() {
    return {
      messages: db.collection('messages').orderBy('createdAt')
    }
  }
}
</script>