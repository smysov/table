<template>
  <div class="wrapper">
    <div class="wrapper__content">
      <section class="restaurants">
        <div class="container">
          <main-table v-bind="{ fields, isShowParameters }"
            :restaurants="performSorting"
            @hideShowCell="hideShowCell"
            @onShowParameters="onShowParameters"
            @sort="sort" />
        </div>
      </section>
    </div>
    <transition name="scale">
      <modal-warning @onHideModal="onHideModal"
        v-show="isShowModal" />
    </transition>
  </div>
</template>

<script>
import MainTable from '@/components/Table.vue';
import ModalWarning from '@/components/ModalWarning.vue';

export default {
  name: 'App',
  components: { MainTable, ModalWarning },
  data() {
    return {
      restaurants: [],
      fields: [
        {
          key: 'business_name',
          name: 'Название ресторана',
          visible: true,
        },
        {
          key: 'business_address',
          name: 'Адрес ресторана',
          visible: true,
        },
        {
          key: 'business_city',
          name: 'Город',
          visible: true,
        },
        {
          key: 'business_phone_number',
          name: 'Телефон ресторана',
          visible: true,
        },
        {
          key: 'inspection_date',
          name: 'Дата инстпекции',
          visible: true,
        },
        {
          key: 'inspection_description',
          name: 'Статус инспекции',
          visible: true,
        },
        {
          key: 'inspection_type',
          name: 'Тип проведения',
          visible: true,
        },
      ],
      isShowModal: false,
      isShowParameters: false,
      currentSortName: 'business_name',
      currentSortDir: 'asc',
    };
  },
  async mounted() {
    try {
      const response = await fetch('/data/restaurants.json');
      const data = await response.json();
      this.restaurants = data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    hideShowCell(key) {
      const findIndex = this.fields.findIndex((item) => item.key === key);
      this.fields[findIndex].visible = !this.fields[findIndex].visible;
      const limit = this.fields.filter((item) => item.visible === false);

      if (limit.length > 6) {
        this.fields[findIndex].visible = true;
        this.isShowModal = true;
        this.isShowParameters = false;
      }
    },
    onHideModal() {
      this.isShowModal = false;
    },
    onShowParameters() {
      this.isShowParameters = !this.isShowParameters;
    },
    sort(key) {
      if (this.currentSortName === key) {
        this.currentSortDir = this.currentSortDir === 'asc' ? 'desc' : 'asc';
      }
      this.currentSortName = key;
    },
    sortingRestaurants() {
      return this.restaurants.sort((a, b) => {
        if (this.currentSortDir === 'desc') return -1;
        if (a[this.currentSortName] < b[this.currentSortName]) return -1;
        if (a[this.currentSortName] > b[this.currentSortName]) return 1;
        return 0;
      });
    },
  },
  computed: {
    performSorting() {
      return this.sortingRestaurants();
    },
  },
};
</script>

<style lang="scss">
.restaurants {
  min-height: 100vh;
  display: flex;
  align-items: center;
}

.scale-enter-active {
  transition: all 0.4s ease-out;
}

.scale-leave-active {
  transition: all 0.2s ease-out;
}

.scale-enter,
.scale-leave-to {
  transform: scale(1.1);
  opacity: 0.6;
}
</style>
