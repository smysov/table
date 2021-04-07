<template>
  <div class="wrapper">
    <div class="wrapper__content">
      <section class="restaurants">
        <div class="container">
          <add-new-restaurants
            @onSubmit="onSubmit"
            :restaurant="restaurant"
            :messageValidation="messageValidation"
          />
          <Table :restaurants="restaurants" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Table from '@/components/Table.vue';
import AddNewRestaurants from '@/components/AddNewRestaurants.vue';

export default {
  name: 'App',
  components: { Table, AddNewRestaurants },
  data() {
    return {
      restaurants: [],
      restaurant: {
        name: '',
        address: '',
        city: '',
        date: '',
        description: '',
      },
      messageValidation: '',
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
  methods: {
    onSubmit() {
      const {
        name, address, city, date, description,
      } = this.restaurant;

      if (!name || !address || !city || !date || !description) {
        this.messageValidation = 'Заполните все поля!';
        return;
      }

      this.restaurants.push({
        _id: {
          $oid: Math.random()
            .toString()
            .slice(2, 8),
        },
        business_name: name,
        business_address: address,
        business_city: city,
        inspection_date: date,
        inspection_description: description,
      });

      this.restaurant.name = '';
      this.restaurant.address = '';
      this.restaurant.city = '';
      this.restaurant.date = '';
      this.restaurant.description = '';
      this.messageValidation = '';
    },
  },
};
</script>

<style lang="scss">
.restaurants {
  min-height: 100vh;
  display: flex;
  align-items: center;
}
</style>
