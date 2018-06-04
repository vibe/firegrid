<template>
    <div class="grid">
      <transition-group name="fade">
        <Item v-for="item in items" :key="item.id" :item="item" />
      </transition-group>
    </div>
</template>

<script>
import Item from "./item.vue";

export default {
  props: ['items'],
  components: {
    Item
  }
};
</script>
<style scoped>
.grid, span {
  display: flex;
  max-width: 100%;
  flex-wrap: wrap;
  background: #eee;
  flex: 3;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
.fade-leave-active {
  position: absolute;
}
.fade-move {
  transition: transform .5s;
}
</style>


