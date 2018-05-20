<template>
<div id="add">
  <!-- 条件付きレンダリング -->
  <Home v-if="!isLogin"></Home>
  <!-- userDataをEditor.vueに引き渡し -->
  <Editor v-if="isLogin" :user="userData"></Editor>
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
      isLogin: false, // Home or Editor 画面切り替え
      userData: null
    }
  },
  // createdは、Vue.jsがそのコンポーネントを作ったタイミングで、実行される。
  created: function() {
    firebase.auth().onAuthStateChanged(user => {
      console.log(user);

      // thisはvueComponent
      if (user) {
        this.isLogin = true;
        this.userData = user;
      } else {
        this.isLogin = false;
        this.userData = null;
      }
    });
  },
  components: {
    // コンポーネントの定義 → <template>内でHTMLタグの用に使える
    'Home': Home,
    'Editor': Editor
  }
}
</script>
