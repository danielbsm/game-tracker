<template>
  <v-layout column>
    <section :class="isMobile && 'text-center'">
      <span class="text-offers">Ofertas </span>
      <v-row class="ma-0 justify-space-between">
        <div :class="isMobile && 'd-flex align-end'">
          <v-text-field
            v-model="search"
            background-color="primary"
            placeholder="Procurar"
            prepend-inner-icon="mdi-magnify"
            outline
            class="input-search"
            color="accent"
            clearable
            solo
            hide-details
          />
        </div>
        <div :class="isMobile && 'd-flex flex-column'">
          <span class="text-sortBy" :class="!isMobile && 'mr-5'"
            >Ordenar por:</span
          >
          <v-menu rounded="t-0" offset-y transition="slide-y-transition">
            <template #activator="{ on, attrs }">
              <v-btn
                color="primary"
                v-bind="attrs"
                height="50"
                width="43vw"
                max-width="180px"
                :class="isMobile && 'font-order-by'"
                v-on="on"
              >
                {{ orderSelected.title }} <v-icon>mdi-chevron-down</v-icon>
              </v-btn>
            </template>
            <v-list color="primary">
              <v-list-item v-for="item in sortBy" :key="item.type" class="pa-0">
                <v-btn
                  :class="isMobile && 'font-order-by'"
                  height="50"
                  width="43vw"
                  max-width="180px"
                  text
                  plain
                  @click="order(item)"
                >
                  {{ item.title }}
                </v-btn>
              </v-list-item>
            </v-list>
          </v-menu>
        </div>
      </v-row>
    </section>
    <v-row class="ma-0 mb-8" justify="center">
      <card-game
        class="mb-5"
        :products-data="products"
        :search="search"
        :order="orderSelected.type"
      />
      <v-col cols="12" class="pa-0">
        <v-row class="ma-0" justify="center">
          <v-btn
            class="px-0"
            color="primary"
            max-width="380"
            width="100%"
            height="50"
            :loading="loading"
            :disabled="loading"
            @click="loadingMore"
            >Carregar mais</v-btn
          >
        </v-row>
      </v-col>
    </v-row>
  </v-layout>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      loading: false,
      search: '',
      sortBy: [
        {
          title: '% de Desconto',
          type: 'savings',
        },
        {
          title: 'Maior preço',
          type: 'biggestPrice',
        },
        {
          title: 'Menor preço',
          type: 'lowestPrice',
        },
        {
          title: 'Título',
          type: 'title',
        },
      ],
      orderSelected: {
        title: '% de Desconto',
        type: 'savings',
      },
      products: [],
      page: 1,
    }
  },
  computed: {
    isMobile() {
      return (
        this.$vuetify.breakpoint.name === 'sm' ||
        this.$vuetify.breakpoint.name === 'xs'
      )
    },
  },
  async created() {
    await this.$gameTrackerApi
      .get('deals?pageNumber=1&pageSize=12&storeID=1&onSale=1&AAA=1')
      .then(({ data }) => {
        console.log(data)
        this.products = data
      })
      .catch((error) => {
        this.$toast.error(
          'Não foi possível realizar a solicitação, por favor tente novamente mais tarde'
        )
        throw new Error(error)
      })
  },
  methods: {
    order(sortBy) {
      this.orderSelected = sortBy
      console.log(sortBy)
      console.log('orderSelected', this.orderSelected)
    },
    async loadingMore() {
      this.page += 1
      this.loading = true
      await this.$gameTrackerApi
        .get(
          `deals?pageNumber=${this.page}&pageSize=12&storeID=1&onSale=1&AAA=1`
        )
        .then(({ data }) => {
          this.products.push(...data)
        })
        .catch((error) => {
          this.$toast.error(
            'Não foi possível carregar mais jogos, por favor tente novamente.'
          )
          throw new Error(error)
        })
        .finally(() => {
          this.loading = false
        })
      console.log(this.products)
    },
  },
}
</script>
<style lang="scss" scoped>
.input-search {
  max-width: 380px;
  width: 50vw;
}

.text-offers {
  font-size: 3.6rem;
  font-weight: 300;
  font-style: normal;
}
.text-sortBy {
  font-size: 1.8rem;
  font-weight: 700;
}
.font-order-by {
  font-size: 1.4rem !important;
}
</style>
