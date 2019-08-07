<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'home' }">Home</router-link>|
      <router-link v-if="!auth" :to="{ name: 'signup' }">Sign Up</router-link>|
      <router-link v-if="!auth" :to="{ name: 'signin' }">Sign In</router-link>|
      <router-link v-if="auth" :to="{ name: 'dashboard' }"
        >Dashboard</router-link
      >
      <a v-if="auth" class="logout" @click="logout">Logout</a>
    </div>
    <div v-if="error" class="error">{{ error }}</div>
    <router-view />
  </div>
</template>
<script>
import { mapState, mapActions, mapGetters } from "vuex";
export default {
  computed: {
    ...mapState(["error"]),
    ...mapGetters({
      auth: "isAuthenticated"
    })
  },
  methods: {
    ...mapActions(["clearError", "logout", "autoLogin"])
  },
  created() {
    this.autoLogin();
  }
};
</script>
<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 1024px;
  margin: 0 auto;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  border-right: 1px solid;
  padding: 0 10px;
}

#nav a:last-child {
  border: none;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.error {
  background-color: rosybrown;
  padding: 20px;
}
</style>
