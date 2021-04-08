<template>
  <tr :style="setBackgroundByStatus">
    <template v-for="field of fields">
      <td class="table-info__description" v-if="field.visible" :key="field.key">
        {{ restaurant[field.key] }}
      </td>
    </template>
  </tr>
</template>

<script>
export default {
  name: 'RestaurantsList',
  props: {
    fields: {
      type: Array,
      required: true,
    },
    restaurant: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      status: {
        'NO ACTION': '#6cf590',
        'REINSPECTION REQUIRED': '#fcef95',
        'SHORTER DATE ADVANCE': '#ff7070',
        'ISSUED PERMIT': '#b1cefc',
      },
    };
  },
  computed: {
    setBackgroundByStatus() {
      return {
        'background-color': this.status[this.restaurant.inspection_description],
      };
    },
  },
};
</script>
