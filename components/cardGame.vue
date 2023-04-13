<template>
  <v-row class="ma-0 justify-space-between">
    <v-card
      v-for="i in 12"
      :key="i"
      color="primary"
      class="ma-0 mb-5 custom-elevation rounded-lg"
      max-width="380px"
      width="99vw"
    >
      <v-img height="147" :src="'/bg-game-card/bg (' + i + ').jpg'"></v-img>
      <v-card-title>RollerCoaster Tycoon® 3: Comp...</v-card-title>
      <v-card-actions class="px-4">
        <v-btn
          class="text-uppercase font-weight-bold rounded-lg"
          color="secondary"
          height="39"
          width="116"
          >Detalhes</v-btn
        >
        <v-row class="ma-0 justify-end">
          <div class="price">
            <div class="old">$ 49,99</div>
            <div class="new">$ 84,59</div>
          </div>
          <div class="discount">-50%</div>
        </v-row>
      </v-card-actions>
    </v-card>
  </v-row>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
::v-deep .v-card__title {
  font-size: 2.4rem !important;
  font-weight: 300 !important;
  line-height: 28.13px !important;
}
.price {
  display: flex;
  flex-direction: column;
  .old {
    text-align: center;
    text-decoration: line-through;
    font-size: 1.2rem;
  }
  .new {
    font-size: 1.8rem;
    font-weight: 700;
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
  font-size: 1.8rem;
  font-weight: 700;
  border-radius: 8px;
  margin-left: 10px;
}
</style>
