<script>
export default {
  name: 'Logout',
  methods: {
    LogOut () {
      try {
        const token = localStorage.getItem('token')
        if (token) {
          this.axios.defaults.headers.common.Authorization = `token ${token}`
        }
        this.axios
          .post('http://127.0.0.1:8000/auth/token/logout/')
          .then(response => {
            localStorage.removeItem('token')
            this.$router.push('/log/')
          })
      } catch (e) {
        console.error('AN API ERROR', e)
      }
    }
  },
  created () {
    this.LogOut()
  }
}
</script>