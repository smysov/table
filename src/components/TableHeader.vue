<template>
  <thead>
    <tr class="table-info">
      <th class="table-info__title" v-for="field of fields" :key="field.key">
        {{ field.name }}
      </th>
    </tr>
  </thead>
</template>

<script>
export default {
  name: 'TableHeader',
  props: {
    fields: {
      type: Array,
      required: true,
    },
  },
};
</script>
