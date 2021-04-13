<template>
  <tr>
    <td class="table-info__quantity"
        colspan="7"> Всего элементов: {{ count }} </td>
  </tr>
</template>

<script>
export default {
  name: 'TableFooter',
  props: {
    count: {
      type: Number,
      require: true,
    },
  },
};
</script>
