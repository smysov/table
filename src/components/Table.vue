<template>
  <div class="table-wrapper"
    ><table class="table-info">
      <thead>
        <tr>
          <th class="table-info__title">
            Название ресторана
          </th>
          <th class="table-info__title">
            Адрес ресторана
          </th>
          <th class="table-info__title">
            Номер ресторана
          </th>
          <th class="table-info__title">
            Город
          </th>
          <th class="table-info__title">
            Дата инспекции
          </th>
          <th class="table-info__title">
            Статус инспекции
          </th>
        </tr>
      </thead>
      <!--Body-->
      <restaurants :restaurants="restaurants" />
      <tfoot>
        <tr>
          <td class="table-info__quantity" colspan="6"
            >Всего элементов: {{ restaurantsLength }}</td
          >
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script>
import Restaurants from '@/components/Restaurants.vue';

export default {
  name: 'Table',
  components: { Restaurants },
  data: () => ({
    restaurants: null,
  }),
  async mounted() {
    try {
      const response = await fetch('/data/restaurants.json');
      const data = await response.json();
      this.restaurants = data;
      console.log(this.restaurants);
    } catch (error) {
      console.log(error);
    }
  },
  computed: {
    restaurantsLength() {
      return this.restaurants.length;
    },
  },
};
</script>

<style lang="scss">
.table-wrapper {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.table-info {
  font-weight: 400;
  text-align: center;
  border: 1px solid #000;
  border-collapse: collapse;
  max-width: 1334px;

  &__title {
    position: relative;
    font-size: 24px;
    font-weight: 400;
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

  &__descripthion {
    position: relative;
    font-size: 20px;
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
