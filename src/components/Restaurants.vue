<template>
  <tbody>
    <tr v-for="restaurant of restaurants" :key="restaurant._id.$oid">
      <td class="table-info__description" v-for="field of fields" :key="field.key">
        {{ restaurant[field.key] }}
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
      required: true,
    },
    fields: {
      type: Array,
      required: true,
    },
  },
};
</script>
