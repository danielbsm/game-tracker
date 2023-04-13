<template>
  <v-layout column>
    <section>
      <span class="text-offers">Ofertas</span>
      <v-row class="ma-0 mt-6 justify-space-between">
        <v-text-field
          background-color="primary"
          placeholder="Procurar"
          prepend-inner-icon="mdi-magnify"
          outlined
          class="input-search rounded-lg"
          color="accent"
          clearable
          solo
        />
        <div class="ma-0 sortby">
          <span class="mr-5">Ordenar por:</span>
          <v-menu rounded="b-xl" offset-y transition="slide-y-transition">
            <template #activator="{ on, attrs }">
              <v-btn
                class="rounded-lg"
                color="primary"
                v-bind="attrs"
                height="50"
                v-on="on"
              >
                % de Desconto <v-icon>mdi-chevron-down</v-icon>
              </v-btn>
            </template>
            <v-list color="primary">
              <v-list-item v-for="i in 4" :key="i" class="pa-0">
                <v-btn height="50" width="100%" text plain> Maior preço </v-btn>
              </v-list-item>
            </v-list>
          </v-menu>
        </div>
      </v-row>
    </section>
    <v-row class="ma-0 mb-8" justify="center">
      <card-game class="mb-5" />
      <v-btn
        class="text-h5 px-0"
        color="primary"
        max-width="380"
        width="100%"
        height="50"
        >Carregar mais</v-btn
      >
    </v-row>
  </v-layout>
</template>

<script>
export default {
  name: 'IndexPage',
}
</script>
<style lang="scss" scoped>
::v-deep .v-icon.v-icon {
  color: var(#fff);
  margin-right: 10px;
}
.input-search {
  max-width: 380px;
  width: 100%;
}
.v-list-item .v-btn .v-btn--plain {
  color: #fff;
  :hover {
    color: var(--v-secondary-base) !important;
  }
}
.v-btn--plain:not(.v-btn--active):not(.v-btn--loading):not(:focus):not(:hover)
  .v-btn__content {
  opacity: 1 !important;
}
.text-offers {
  font-size: 3.6rem;
}
.sortby {
  span {
    font-size: 1.8rem;
    font-weight: 700;
  }
}
.text-teste {
  font-size: 1.8rem;
  font-weight: 100;
}
</style>
