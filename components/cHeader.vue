<template>
  <v-app-bar elevation="0" app fixed color="primary"> </v-app-bar>
</template>
<script>
export default {
  data() {
    return {
      menu: [
        {
          title: 'Inicio',
          to: '/',
        },
        {
          title: 'Mais lidos',
          to: '/mais-lidos',
        },
        {
          title: 'Autores',
          to: '/autores',
        },
      ],
      currentLocate: {
        lang: 'Português',
        flag: 'brazil-flag.png',
        key: 'pt-BR',
      },
      locales: [
        {
          lang: 'Português',
          flag: 'brazil-flag.png',
          key: 'pt-BR',
        },
        {
          lang: 'Español',
          flag: 'spain-flag.png',
          key: 'SPN',
        },
        {
          lang: 'English',
          flag: 'usa-flag.png',
          key: 'eua',
        },
      ],
    }
  },
  methods: {
    menuClick(route) {
      this.$router.push(route)
    },
  },
}
</script>
<style lang="scss">
.v-toolbar__content {
  width: 100%;
  max-width: 1185px !important;
  padding: 0 12px !important;
}
.brand {
  font-size: 25px;
  font-weight: bold;
  background: rgb(104, 102, 138);
  background: linear-gradient(
    7deg,
    rgba(104, 102, 138, 1) 1%,
    rgba(99, 99, 222, 1) 50%,
    rgba(19, 95, 111, 1) 100%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  cursor: pointer;
}
</style>
