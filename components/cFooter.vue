<template>
  <v-footer color="primary" class="pa-0">
    <v-container>
      <v-row class="ma-0 justify-center"
        ><svg-brand :class="!isMobile ? 'mt-15 mb-8' : 'mt-5 mb-4'"
      /></v-row>
      <v-row class="ma-0 mb-5 text-footer">
        © 2021, Game Tracker Inc. Todos os direitos reservados. Nulla facilisi.
        Etiam sagittis congue tempor. Pellentesque habitant morbi tristique
        senectus et netus et malesuada fames ac turpis egestas. Suspendisse eu
        velit et ante luctus egestas. Aenean sed nisi tellus. Duis non ornare
        libero. Quisque suscipit maximus nisi, in gravida felis. Cras ornare
        mauris ac nisi congue, ut condimentum sem tincidunt. Phasellus semper
        tellus malesuada turpis gravida cursus. Duis nec eleifend nunc, vitae
        finibus elit. Aliquam eget diam vitae purus suscipit viverra.
      </v-row>
      <div
        class="d-flex ma-0 links"
        :class="isMobile ? 'flex-column text-center mb-4' : 'mb-15'"
      >
        <a href="#">Termos de Serviço</a>
        <a href="#">Política de Privacidade</a>
        <a href="#">Trabalhe conosco</a>
        <a href="#">Contato</a>
      </div>
    </v-container>
  </v-footer>
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
<style lang="scss">
.text-footer {
  font-size: 1.4rem;
  @media screen and (max-width: 768px) {
    text-align: center;
    font-size: 1rem;
  }
}
.links a {
  color: #fff !important;
  text-decoration: none;
  margin-right: 46px;
  font-size: 1.4rem;
  font-weight: 700;
  @media screen and (max-width: 768px) {
    margin-right: 0;
    margin-top: 8px;
    font-size: 1.2rem;
  }
}
</style>
