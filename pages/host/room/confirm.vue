<template lang="pug">
  v-container.blue-gradient
    v-row(justify="center" no-gutters)
      v-col(cols="11")
        v-row.mt-6
          v-col
            h2.white--text
              | In the category,
              br
              | there are...
        v-row.images.mt-6
          v-col.pa-0(cols="4" v-for="avatar in avatars" :key="avatar")
            v-img(:src="getPicture(avatar)")
        v-row.mt-6(justify="center")
          v-col(cols="10")
            v-btn(color="black" :block="true" @click="submit")
              span.white--text Create a Room
        v-row(justify="center")
          v-col(cols="10")
            v-btn(to="/host/room" color="grey" :block="true" nuxt)
              span.white--text Back
</template>

<script>
export default {
  data () {
    return {
      category: this.$route.query.category,
      avatars: ['1', '2', '3', '4', '5', '6', '7', '8', '9'],
      selected: ''
    }
  },
  methods: {
    getPicture (avatar) {
      return `/images/avatars/${this.category}/${avatar}.jpg`
    },
    selectAvatar (avatar) {
      this.selected = avatar
    },
    isSelected (avatar) {
      return avatar === this.selected
    },
    async submit () {
      this.$nuxt.$loading.start()
      await this.$axios.$post('/sleeves', { category: this.category })
        .then((data) => {
          this.$nuxt.$loading.finish()
          this.$router.push({ path: '/host/room/complete', query: { roomId: data.roomId } })
        })
    }
  }
}
</script>

<style scoped>
.images {
  opacity: 0.8;
}
</style>
