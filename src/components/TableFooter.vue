<template>
  <tr>
    <td class="table-info__quantity" colspan="7">
      Всего элементов: {{ restaurantsLength }}
    </td>
  </tr>
</template>

<script>
export default {
  name: 'TableFooter',
  props: {
    restaurants: {
      type: Array,
      require: true,
    },
  },
  computed: {
    restaurantsLength() {
      return this.restaurants.length;
    },
  },
};
</script>
