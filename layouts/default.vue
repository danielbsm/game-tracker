<template>
  <v-app>
    <c-header />
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <c-footer />
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
}
</script>
<style lang="scss" scoped>
::v-deep .v-main {
  margin-top: 45px;
}
</style>
