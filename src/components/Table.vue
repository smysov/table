<template>
  <div class="table-wrapper">
    <header-opportunities
      @onShowParameters="onShowParameters"
      @search="search = $event"
      :isShowParameters="isShowParameters"
      :value="search"
    />
    <table class="table-info" @click="isShowParameters = false">
      <!--Header-->
      <table-header />
      <!--Body-->
      <restaurants :restaurants="searchByParameters" @deleteInfo="deleteInfo" />
      <!--Footer-->
      <table-footer :restaurants="searchByParameters" />
    </table>
  </div>
</template>

<script>
import Restaurants from '@/components/Restaurants.vue';
import TableHeader from '@/components/TableHeader.vue';
import TableFooter from '@/components/TableFooter.vue';
import HeaderOpportunities from '@/components/HeaderOpportunities.vue';

export default {
  name: 'MainTable',
  components: {
    Restaurants,
    TableHeader,
    TableFooter,
    HeaderOpportunities,
  },
  data: () => ({
    isShowParameters: false,
    search: '',
  }),
  props: {
    restaurants: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    searchByParameters() {
      const { search, restaurants } = this;
      const value = search.trim().toUpperCase();

      if (!search) return restaurants;

      const sortedRestaurants = restaurants.filter((item) => {
        if (
          item.business_name.indexOf(value) !== -1
          || item.business_address.indexOf(value) !== -1
          || item.business_city.indexOf(value) !== -1
          || item.business_phone_number.indexOf(value) !== -1
          || item.inspection_date.indexOf(value) !== -1
          || item.inspection_description.indexOf(value) !== -1
        ) {
          return item;
        }
      });

      return sortedRestaurants;
    },
  },
  methods: {
    onShowParameters() {
      this.isShowParameters = !this.isShowParameters;
    },
  },
};
</script>

<style lang="scss">
.table-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  border: 1px solid #000;
  max-width: 1334px;
  margin: 0 auto;
}

.table-info {
  font-weight: 400;
  text-align: center;
  border-collapse: collapse;

  &__title {
    position: relative;
    font-size: 24px;
    font-weight: 400;
    width: 20%;
    padding: 15px 17px;
    color: #000;
    border-top: 1px solid rgba(0, 0, 0, 1);
    border-bottom: 3px solid rgba(0, 0, 0, 0.5);

    &::before {
      position: absolute;
      content: '';
      top: 50%;
      right: 0;
      height: 40px;
      width: 3px;
      background-color: #000;
      transform: translateY(-50%);
    }

    &:last-child::before {
      display: none;
    }
  }

  &__description {
    position: relative;
    font-size: 20px;
    text-transform: uppercase;
    padding: 15px 18px;
    color: #1f1f1f;
    border-bottom: 1px solid rgba(0, 0, 0, 0.5);

    &::before {
      position: absolute;
      content: '';
      top: 50%;
      right: 0;
      height: 40px;
      width: 1px;
      background-color: #000;
      transform: translateY(-50%);
    }

    &:last-child::before {
      display: none;
    }
  }

  &__quantity {
    font-size: 16px;
    text-align: right;
    padding: 10px 30px 10px 0;
  }
}
</style>
