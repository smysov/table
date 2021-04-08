<template>
  <div class="wrapper">
    <div class="wrapper__content">
      <section class="restaurants">
        <div class="container">
          <main-table :restaurants="restaurants" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import MainTable from '@/components/Table.vue';

export default {
  name: 'App',
  components: { MainTable },
  data() {
    return {
      restaurants: [],
    };
  },
  async mounted() {
    try {
      const response = await fetch('/data/restaurants.json');
      const data = await response.json();
      this.restaurants = data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {},
};
</script>

<style lang="scss">
.restaurants {
  min-height: 100vh;
  display: flex;
  align-items: center;
}
</style>
