<template lang="pug">
  v-container.blue-gradient
    v-row(justify="center" no-gutters)
      v-col(cols="11")
        v-row.mt-6
          v-col
            h2.white--text
              | Today, I identify
              br
              | most with this picture...
        v-row.mt-6
          v-col(align="center")
            v-img(:src="picture" width="350" height="350")
        v-row.mt-6
          v-col(align="center")
            v-text-field(
              solo
              counter
              placeholder="I chose this picture because..."
              v-model="feeling"
              maxlength="80")
        v-row(justify="center")
          v-col(cols="10")
            v-btn(color="black" :block="true" @click="submit")
              span.white--text That's the One!
        v-row(justify="center")
          v-col(cols="10")
            v-btn(:to="{ path: '/guest/picture', query: this.$route.query }" color="grey" :block="true" nuxt)
              span.white--text Back
</template>

<script>
export default {
  data () {
    return {
      feeling: ''
    }
  },
  computed: {
    picture () {
      return `/images/avatars/${this.$route.query.category}/${this.$route.query.avatarId}.jpg`
    }
  },
  methods: {
    async submit () {
      this.$nuxt.$loading.start()
      await this.$axios.$patch('/sleeves/' + this.$route.query.roomId, {
        nickName: this.$route.query.nickName,
        avatarId: this.$route.query.avatarId,
        feeling: this.feeling
      })
        .then((data) => {
          this.$nuxt.$loading.finish()
          this.$router.push('/guest/complete')
        })
        .catch(() => {
          alert('Sorry something\'s wrong.')
        })
    }
  }
}
</script>
