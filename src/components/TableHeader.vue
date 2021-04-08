<template>
  <thead>
    <tr class="table-info">
      <th class="table-info__title" v-for="field of visibleCell" :key="field.key">
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
  computed: {
    visibleCell() {
      return this.fields.filter((item) => item.visible === true);
    },
  },
};
</script>
