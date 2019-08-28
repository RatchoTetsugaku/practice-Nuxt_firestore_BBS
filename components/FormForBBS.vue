<template>
  <div>
    <!--フォームの表示ボタン-->
    <v-btn color="blue" center fixed right @click="showCreateForm">投稿</v-btn>
    <v-dialog v-model="displayForm" max-width="500px">
      <v-card>
        <v-container>
          <h2>メッセージ入力</h2>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field v-model="inputComment" :rules="commentRules" label="メッセージ" required></v-text-field>
            <v-btn :disabled="!valid" @click="addComment">書き込む</v-btn>
          </v-form>
        </v-container>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import { db } from '~/plugins/firebase.js'

export default {
  name: 'FormForBBS',
  data: () => ({
    // form入力データ
    inputComment: '',
    // バリデーション
    valid: true,
    commentRules: [v => !!v || 'メッセージは必須項目です'],
    // Formダイアログの表示可否
    displayForm: false
  }),
  methods: {
    // コメント追加
    addComment() {
      const now = new Date()
      // コメントをFirestoreへ登録
      db.collection('messages').add({
        content: this.inputComment,
        avatar:
          'https://picsum.photos/50?image=' +
          (Math.floor(Math.random() * 400) + 1),
        createdAt: now
      })
      // ダイアログを閉じる
      this.hideCreateForm()
    },
    // Formの初期化
    clear() {
      this.$refs.form.reset()
    },
    // Formダイアログの表示
    showCreateForm() {
      this.displayForm = true
    },
    //
    // Formダイアログの非表示
    hideCreateForm() {
      this.clear()
      this.displayForm = false
    }
  }
}
</script>
