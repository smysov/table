<template>
  <tbody>
    <tr v-for="restaurant of restaurants" :key="restaurant._id.$oid">
      <td class="table-info__descripthion">
        {{ restaurant.business_name }}
      </td>
      <td class="table-info__descripthion">
        {{ restaurant.business_location }}
      </td>
      <td class="table-info__descripthion">
        {{ restaurant.business_phone_number || 'Not found' }}
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
    </tr>
  </tbody>
</template>

<script>
export default {
  name: 'RestaurantsList',
  props: {
    restaurants: {
      type: Array,
      default: () => [],
    },
  },
};
</script>
