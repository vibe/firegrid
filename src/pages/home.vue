<template>
  <div class="page">
    <header>
      <div class="logo">
        <img src="public/img/logo.png" alt="Las Vegas Top Real Estate Agent" />
      </div>
      <h1>Kevin Johnson - Las Vegas Top Real Estate Agent</h1>
    </header>
    <section class="grid-wrapper">
      <Grid :items="items"/>
      <Filters @applyPriceFilters="applyPriceFilters" @applyBedFilters="applyBedFilters" @applyBathFilters="applyBathFilters" @applyAreaFilters="applyAreaFilters" @applyViewFilter="applyViewFilter" />
    </section>
  </div>
</template>


<script>
import Grid from "../components/grid.vue";
import Filters from "../components/filters.vue";
import houses from "../data/houses.json";

export default {
  components: {
    Grid,
    Filters
  },
  data: function() {
    return {
      items: houses
    }
  },
  methods: {
    applyPriceFilters(filters) {
      this.items = houses.filter(house => {
        if(house.price >= filters.maxPrice) {
          return false;
        }
        return true;
      }).filter(house => house.price >= filters.minPrice);
    },
    applyBedFilters(filters) {
      this.items = houses.filter(house => house.bedrooms >= filters.minBed)
                         .filter(house => house.bedrooms <= filters.maxBed);
    },
    applyBathFilters(filters) {
      this.items = houses.filter(house => house.baths >= filters.minBath)
                         .filter(house => house.baths <= filters.maxBath);
    },
    applyAreaFilters(filters) {
      this.items = houses.filter(house => house.area >= filters.minArea)
                         .filter(house => house.area <= filters.maxArea);      
    },
    applyViewFilter(value) {
      this.items = houses.filter(house => house.view == value);
    }
  }
};
</script>

<style scoped>
header {
  background: transparent url("/public/img/header.jpg") no-repeat center bottom;
  display: flex;
  flex-direction: row;
  align-items: center;
}

header .logo {
  width: 180px;
  padding: 20px;
  position: relative;
  top: 50px;
}
header img {
  display: block;
  max-width: 100%;
}
header h1 {
  color: #fff;
  display: block;
}
.grid-wrapper {
  padding: 50px 0;
  display: flex;
  width: 100%;
}

</style>
