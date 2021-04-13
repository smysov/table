<template>
  <tr class="table-info">
    <th class="table-info__title"
        @click="sort(field.key)"
        v-for="(field, index) of visibleCell"
        :key="index">
      {{ field.name }}
    </th>
  </tr>
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
  methods: {
    sort(key) {
      this.$emit('sort', key);
    },
  },
};
</script>
