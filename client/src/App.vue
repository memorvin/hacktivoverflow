<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  computed: {
    error() {
      return this.$store.state.error
    },
    success() {
      return this.$store.state.success
    },
    errorCount() {
      return this.$store.state.errorCount
    },
    successCount() {
      return this.$store.state.successCount
    },
    user() {
      return this.$store.state.userCount
    }
  },
  watch: {
    errorCount() {
      this.alertError()
    },
    successCount() {
      this.alertSuccess()
    }
  },
  methods: {
    alertError() {
      this.$swal.fire({
        icon: 'error',
        title: 'Error',
        text: this.error,
      })
    },
    alertSuccess() {
      this.$swal.fire({
        icon: 'success',
        title: 'Success',
        text: this.success,
      })
    }
  },
  created() {
    if (!localStorage.getItem('access_token')) {
      this.$router.push('/landing').catch(() => {})
    }
    this.$store.dispatch('fetchQuestions')
    this.$store.dispatch('fetchWatchedTags')
  },
  
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Fjalla+One|Noto+Sans&display=swap');

#app {
  font-family: 'Noto Sans', sans-serif;
  /* font-family: 'Fjalla One', sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
