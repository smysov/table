<template>
  <tbody>
    <tr v-for="(restaurant, index) of restaurants" :key="restaurant._id.$oid">
      <td class="table-info__descripthion">
        {{ restaurant.business_name }}
      </td>
      <td class="table-info__descripthion">
        {{ restaurant.business_address }}
      </td>
      <td class="table-info__descripthion">
        {{ restaurant.business_city }}
      </td>
      <td class="table-info__descripthion">
        {{ restaurant.inspection_date }}
      </td>
      <td class="table-info__descripthion">
        {{ restaurant.inspection_description }}
      </td>
      <td class="table-info__descripthion">
        <button
          @click="deleteInfo(index)"
          class="table-info__hide"
          aria-label="Скрыть"
        ></button>
      </td>
    </tr>
  </tbody>
</template>

<script>
export default {
  name: 'RestaurantsList',
  props: {
    restaurants: {
      type: Array,
      default: () => ([]),
    },
  },
  methods: {
    deleteInfo(index) {
      this.$emit('deleteInfo', index);
    },
  },
};
</script>
