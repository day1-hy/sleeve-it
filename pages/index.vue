<template lang="pug">
  v-container
    v-app-bar(fixed app flat color="#e98065" height="70")
      v-row
        v-col(align="center")
          v-img(src="/header.png" width="100" height="60")
    v-row(justify="center")
      v-col(cols="11")
        v-form
          v-row
            v-col
              v-text-field(v-model="id" label="Username or email")
          v-row
            v-col
              v-text-field(v-model="password" label="Password" type="password")
          v-row
            v-col
              v-btn(color="black" :block="true" @click="submit")
                span.white--text Host Log in
          v-row
            v-divider
          v-row
            v-col(align="center")
              p OR
          v-row
            v-col
              v-btn(to="/guest" color="blue" :block="true" nuxt)
                span.white--text Guest
</template>

<script>
export default {
  data () {
    return {
      id: '',
      password: ''
    }
  },
  methods: {
    submit () {
      this.$router.push('/host')
    }
  }
}
</script>
