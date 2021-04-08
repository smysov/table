<template>
  <tbody>
    <tr v-for="restaurant of restaurants" :key="restaurant._id.$oid">
      <template v-for="field of fields">
        <td
        class="table-info__description"
        v-if="field.visible"
        :key="field.key"
        >
          {{ restaurant[field.key] }}
        </td>
      </template>
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
