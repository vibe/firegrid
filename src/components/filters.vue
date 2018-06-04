<template>
    <section class="filters">
        <div class="filter">
            <VueSlider ref="price-range" v-model="price" :max="maxPrice" @callback="applyPriceFilters"/>
        </div>
        <div class="filter">
            <VueSlider ref="area-range" v-model="area" :max="maxArea" @callback="applyAreaFilters"/>
        </div>
        <div class="filter">
            <VueSlider ref="bed-range" v-model="beds" :max="maxBed" @callback="applyBedFilters" :piecewise="true"/>
        </div>
        <div class="filter">
            <VueSlider ref="bath-range" v-model="baths" :max="maxBath" @callback="applyBathFilters" :piecewise="true"/>
        </div>
        <div class="filter">
           <label><input type="checkbox" v-model="hasView" @change="applyViewFilter"><span>with View</span></label>
        </div>
    </section>    
</template>
<script>
import VueSlider from 'vue-slider-component/src/vue2-slider.vue'
import houses from '../data/houses.json';

const maxprice = houses.reduce((max, house) => {
    const newPrice = house.price > max ? house.price : max;
    return newPrice;
}, 0);
const maxbed = houses.reduce((max, house) => {
    return house.bedrooms > max ? house.bedrooms : max;
}, 0);
const maxbath = houses.reduce((max, house) => {
    return house.baths > max ? house.baths : max;
}, 0);
const maxarea = houses.reduce((max, house) => {
    return house.area > max ? house.area : max;
}, 0);
export default {
    components: {
        VueSlider
    },
    data: function() {
        return {
            price: [0, maxprice],
            beds: [0, maxbed],
            baths: [0, maxbath],
            area: [0, maxarea],
            maxPrice: parseInt(maxprice),
            maxBed: parseInt(maxbed),
            maxBath: parseInt(maxbath),
            maxArea: parseInt(maxarea),
            hasView: false,
        }
    },
    methods: {

        applyPriceFilters(values) {
            const [ min, max ] = values;
            this.$emit('applyPriceFilters', {
                minPrice: min,
                maxPrice: max
            })
        },
        applyBedFilters(values) {
            const [min, max] = values;
            this.$emit('applyBedFilters', {
                minBed: min,
                maxBed: max
            });
        },
        applyBathFilters(values) {
            const [ min, max ] = values;
            this.$emit('applyBathFilters', {
                minBath: min,
                maxBath: max
            })
        },
        applyAreaFilters(values) {
            const [ min, max ] = values;
            this.$emit('applyAreaFilters', {
                minArea: min,
                maxArea: max
            });
        },
        applyViewFilter() {
            this.$emit('applyViewFilter', this.hasView);
        }
    }
}
</script>

<style scoped>
    .filters {
        flex: 1;
        padding: 20px;
    }
    .filter {
        padding: 20px 0;
    }
</style>
