<template>
  <div class="wrapper">
    <div class="wrapper__content">
      <section class="restaurants">
        <div class="container">
          <Table />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Table from '@/components/Table.vue';

export default {
  name: 'App',
  components: { Table },
};
</script>
