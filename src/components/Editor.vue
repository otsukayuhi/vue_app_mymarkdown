<template>
<div class="editor">
  <h1>エディター画面</h1>
  <span>{{ user.displayName }}</span>
  <span>{{ user.email }}</span>
  <span class="editor_img"><img v-bind:src="user.photoURL"></span>
  <button @click="logout">ログアウト</button>
  <div class="editorWrap">
    <textarea class="markdown" v-model="markdown"></textarea>
    <div class="preview" v-html="preview()"></div>
  </div>
</div>
</template>

<script>
import marked from 'marked';
export default {
  name: 'editor',
  props: ['user'], // 親コンポーネントから、userを受け継ぐ。
  data () {
    return {
      markdown: ''
    }
  },
  methods: {
    logout: function() {
      firebase.auth().signOut();
    },
    preview: function() {
      return marked(this.markdown);
    }
  }
}
</script>

<style lang="scss" scoped>
.editor_img {
  display: block;
  width: 50px;
  height: 50px;
  img {
    width: 100%;
  }
}
.editorWrap {
  display: flex;
}
.markdown {
  width: 50%;
  height: 500px;
}
.preview {
  width: 50%;
}
</style>
