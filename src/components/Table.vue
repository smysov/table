<template>
  <div class="table-wrapper">
    <header-opportunities @hideShowCell="hideShowCell"
                          @searchInput="performSearch"
                          v-bind="{ fields, searchQuery }" />
    <table class="table-info">
      <!--Header-->
      <thead>
        <table-header @sort="sort"
                      :fields="fields" />
      </thead>
      <!--Body-->
      <tbody>
        <restaurants :fields="fields"
                     v-for="restaurant of visibleRestaurants"
                     :key="restaurant._id.$oid"
                     :restaurant="restaurant" />
      </tbody>
      <!--Footer-->
      <tfoot>
        <table-footer :count="count" />
      </tfoot>
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
    searchQuery: '',
    searchResults: [],
  }),
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
  computed: {
    visibleRestaurants() {
      return this.searchQuery === '' ? this.restaurants : this.searchResults;
    },
    count() {
      return this.visibleRestaurants.length;
    },
  },
  methods: {
    hideShowCell(key) {
      this.$emit('hideShowCell', key);
    },
    performSearch(searchQuery) {
      this.searchQuery = searchQuery;
      const value = this.searchQuery.trim().toLowerCase();

      this.searchResults = this.restaurants.filter((item) => {
        let showItem = false;

        this.fields.forEach((field) => {
          if (field.visible && !showItem) {
            showItem = item[field.key].toLowerCase().includes(value);
          }
        });
        return showItem;
      });
    },
    sort(key) {
      this.$emit('sort', key);
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
    transition: all 0.3s cubic-bezier(0.075, 0.82, 0.165, 1);
    cursor: pointer;

    &:hover {
      color: #7387b3;
    }

    &::before {
      position: absolute;
      content: "";
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
      content: "";
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
