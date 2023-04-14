<template>
  <v-app-bar elevation="5" app fixed color="primary" height="50">
    <v-container>
      <v-row class="ma-0 align-center" :class="isMobile && 'justify-center'">
        <svg-brand />
        <div class="brand ml-3">
          Game <span class="font-weight-bold"> Tracker</span>
        </div>
      </v-row>
    </v-container>
  </v-app-bar>
</template>
<script>
export default {
  computed: {
    isMobile() {
      return (
        this.$vuetify.breakpoint.name === 'sm' ||
        this.$vuetify.breakpoint.name === 'xs'
      )
    },
  },
}
</script>
<style lang="scss" scoped>
.brand {
  font-size: 2.4rem;
}
</style>
