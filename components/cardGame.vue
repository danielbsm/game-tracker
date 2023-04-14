<template>
  <v-layout>
    <v-row v-if="showCards" class="ma-0 justify-space-between">
      <v-col
        v-for="(product, index) in products"
        :key="index"
        cols="12"
        xs="12"
        sm="12"
        md="6"
        lg="4"
        :class="isMobile && 'px-0'"
      >
        <v-card color="primary" class="custom-elevation">
          <img
            width="100%"
            :src="getImage(product.steamAppID)"
            :alt="product.title"
            :height="!isMobile ? 147 : 95"
          />
          <v-card-title class="col-11">{{ product.title }}</v-card-title>
          <v-card-actions class="pa-4" :class="isMobile && 'pt-0'">
            <v-btn
              class="text-uppercase font-weight-bold px-5"
              :class="isMobile && 'font-btn-mobile'"
              color="secondary"
              :height="isMobile ? 30 : 39"
              :width="isMobile ? 92 : 116"
              >Detalhes</v-btn
            >
            <v-row class="ma-0 justify-end">
              <div class="price">
                <div class="old">
                  $ {{ product.normalPrice | formatMoney() }}
                </div>
                <div class="new">$ {{ product.salePrice | formatMoney() }}</div>
              </div>
              <div class="discount">
                -{{ product.savings | formatPercentage }}%
              </div>
            </v-row>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <v-row v-else class="ma-0">
      <not-found />
    </v-row>
  </v-layout>
</template>

<script>
export default {
  filters: {
    formatMoney(value) {
      const formatter = Number(value)
      return formatter.toLocaleString('pt-br', {
        minimumFractionDigits: 2,
      })
    },
    formatPercentage(value) {
      return Math.round(Number(value))
    },
  },
  props: {
    productsData: {
      type: Array,
      required: true,
    },
    search: {
      type: String,
      required: false,
      default: null,
    },
    order: {
      type: String,
      required: true,
    },
  },
  computed: {
    products() {
      if (this.search) {
        const products = this.productsData.filter((product) =>
          product.title.toLowerCase().includes(this.search.toLowerCase())
        )
        return this.sortBy(products)
      }
      return this.sortBy(this.productsData)
    },
    showCards() {
      return this.products.length > 0
    },
    isMobile() {
      return (
        this.$vuetify.breakpoint.name === 'sm' ||
        this.$vuetify.breakpoint.name === 'xs'
      )
    },
  },
  methods: {
    getImage(steamAppID) {
      return (
        'https://cdn.akamai.steamstatic.com/steam/apps/' +
        steamAppID +
        '/header.jpg'
      )
    },
    sortBy(products) {
      if (this.order === 'savings' || this.order === 'biggestPrice') {
        return this.sortByDescending(products)
      } else {
        return this.sortByAscending(products)
      }
    },
    sortByAscending(products) {
      const prop = this.order === 'lowestPrice' ? 'salePrice' : this.order
      products.sort((a, b) => {
        const sortA = this.order === 'lowestPrice' ? Number(a[prop]) : a[prop]
        const sortB = this.order === 'lowestPrice' ? Number(b[prop]) : b[prop]
        if (sortA > sortB) {
          return -1
        }
        if (sortA < sortB) {
          return 1
        }
        return 0
      })
      return products
    },
    sortByDescending(products) {
      const prop = this.order === 'biggestPrice' ? 'salePrice' : this.order
      products.sort((a, b) => {
        const sortA = this.order === 'biggestPrice' ? Number(a[prop]) : a[prop]
        const sortB = this.order === 'biggestPrice' ? Number(b[prop]) : b[prop]
        if (sortA > sortB) {
          return -1
        }
        if (sortA < sortB) {
          return 1
        }
        return 0
      })
      return products
    },
  },
}
</script>

<style lang="scss" scoped>
::v-deep .v-card__title {
  font-size: 2.2rem !important;
  font-weight: 300 !important;
  @media screen and (max-width: 768px) {
    font-size: 1.8rem !important;
  }
}
.price {
  display: flex;
  flex-direction: column;
  .old {
    font-size: 1.2rem;
    font-weight: 100;
    text-align: end;
    text-decoration: line-through;
    @media screen and (max-width: 768px) {
      font-size: 1rem;
    }
  }
  .new {
    font-size: 1.8rem;
    font-weight: 700;
    @media screen and (max-width: 768px) {
      font-size: 1.4rem;
    }
  }
}
.custom-elevation {
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25) !important;
}

.discount {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 84px;
  height: 40px;
  background-color: var(--v-info-base);
  border-radius: 8px;
  margin-left: 10px;
  font-size: 1.8rem;
  font-weight: 700;
  @media screen and(max-width: 400px) {
    width: 64px;
    font-size: 1.4rem;
  }
}
.font-btn-mobile {
  font-size: 1.4rem !important;
}
</style>
