<template>
<div id="add">
  <!-- 条件付きレンダリング -->
  <Home v-if="!isLogin"></Home>
  <Editor v-if="isLogin"></Editor>
</div>
</template>

<script>
// .vueファイル読み込み
import Home from './components/Home';
import Editor from './components/Editor';

export default {
  name: 'app',
  data () {
    return {
      isLogin: false // Home or Editor 画面切り替え
    }
  },
  // createdは、Vue.jsがそのコンポーネントを作ったタイミングで、実行される。
  created: function() {
    firebase.auth().onAuthStateChanged(user => {
      console.log(user);
      if (user) {
        this.isLogin = true;
      } else {
        this.isLogin = false;
      }
      console.log(this.isLogin);

    });
  },
  components: {
    // コンポーネントの定義 → <template>内でHTMLタグの用に使える
    'Home': Home,
    'Editor': Editor
  }
}
</script>
