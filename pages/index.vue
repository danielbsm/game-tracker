<template>
  <v-layout column>
    <section class="page-index">
      <span class="text-offers">Ofertas </span>
      <v-row class="box-filters ma-0 justify-space-between">
        <div class="box-search">
          <v-text-field
            v-model="search"
            background-color="primary"
            placeholder="Procurar"
            prepend-inner-icon="mdi-magnify"
            outline
            color="accent"
            clearable
            solo
            hide-details
          />
        </div>
        <div class="fill-width box-sort">
          <span class="text-sortby" :class="!isMobile && 'mr-5'"
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
                v-on="on"
              >
                {{ orderSelected.title }} <v-icon>mdi-chevron-down</v-icon>
              </v-btn>
            </template>
            <v-list color="primary">
              <v-list-item v-for="item in sortBy" :key="item.type" class="pa-0">
                <v-btn
                  height="35"
                  width="100%"
                  max-width="180px"
                  text
                  plain
                  :class="
                    item.type === orderSelected.type &&
                    'secondary--text font-weight-bold'
                  "
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
            @click="getProducts"
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
      page: 0,
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
  created() {
    this.getProducts()
  },
  methods: {
    order(sortBy) {
      this.orderSelected = sortBy
    },
    async getProducts() {
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
    },
  },
}
</script>
<style lang="scss" scoped>
::v-deep .v-input__control {
  max-width: 380px !important;
  min-width: 174px !important;
  min-height: 50px !important;
  @media screen and (max-width: 400px) {
    min-height: 36px !important;
  }
}
.page-index {
  @media screen and (max-width: 650px) {
    text-align: center;
  }
  .text-offers {
    font-size: 2.6rem;
    font-weight: 300;
    font-style: normal;
  }
  .box-filters {
    width: 100%;

    .box-search {
      width: calc(50% - 10px);
      @media screen and (max-width: 650px) {
        display: flex;
        align-items: end;
        @media screen and (max-width: 370px) {
          max-width: 174px;
          width: 100%;
        }
      }
    }

    .box-sort {
      display: flex;
      justify-content: end;
      align-items: center;
      @media screen and (max-width: 650px) {
        flex-direction: column !important;
        @media screen and (max-width: 400px) {
          button {
            max-height: 36px !important;
            max-width: 122px !important;
            font-size: 1.2rem !important;
          }
          i {
            font-size: 1.4rem;
          }
        }
      }
      .text-sortby {
        font-size: 1.8rem;
        font-weight: 700;
        margin-right: 20px;
        @media screen and (max-width: 650px) {
          margin-right: 0;
          @media screen and (max-width: 400px) {
            font-size: 1.4rem;
            margin-bottom: 4px;
          }
        }
      }
      @media screen and (max-width: 370px) {
        max-width: 122px;
        width: 100%;
      }
    }
  }
}
</style>
