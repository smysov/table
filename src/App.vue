<template>
  <div class="wrapper">
    <div class="wrapper__content">
      <section class="restaurants">
        <div class="container">
          <main-table v-bind="{ restaurants, fields }" />
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
      fields: [
        {
          key: 'business_name',
          name: 'Название ресторана',
        },
        {
          key: 'business_address',
          name: 'Адрес ресторана',
        },
        {
          key: 'business_city',
          name: 'Город',
        },
        {
          key: 'business_phone_number',
          name: 'Телефон ресторана',
        },
        {
          key: 'inspection_date',
          name: 'Дата инстпекции',
        },
        {
          key: 'inspection_description',
          name: 'Статус инспекции',
        },
        {
          key: 'inspection_type',
          name: 'Тип проведения',
        },
      ],
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
