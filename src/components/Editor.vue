<template>
<div class="editor">
  <h1>エディター画面</h1>
  <span>{{ user.displayName }}</span>
  <span>{{ user.email }}</span>
  <span><img v-bind:src="user.photoURL"></span>
  <button @click="logout">ログアウト</button>
</div>
</template>

<script>
export default {
  name: 'editor',
  props: ['user'], // 親コンポーネントから、userを受け継ぐ。
  data () {
    return {
    }
  },
  methods: {
    logout: function() {
      firebase.auth().signOut();
    }
  }
}
</script>

<style lang="sass">
</style>
