<template>
  <div id="app">
    ONLINE USER: {{ online_users }}
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  created () {
    this.intervalData = window.setInterval(() => {
      this.getDataUsersOnline()
    }, 3000)
  },
  data () {
    return {
      online_users: 0,
      intervalData: null,
    }
  },
  beforeDestroy() {
    window.clearInterval(this.intervalData)
  },
  methods: {
    getDataUsersOnline () {
      axios.get('http://localhost:8080/detail/')
        .then((data) => {
          this.online_users = data['data']['online_user']
        })
    }
  }
}
</script>
