<template>
  <form class="add-restaraunts" @submit.prevent="onSubmit">
    <h2 class="add-restaraunts__title">Добавить новый ресторан</h2>
    <p class="add-restaraunts__error" v-show="messageValidation">
      {{ messageValidation }}
    </p>
    <div class="add-restaraunts__row">
      <div class="add-restaraunts__cell">
        <label class="add-restaraunts__subtitle" for="name">Название ресторана</label>
        <input
          v-model="restaurant.name"
          class="add-restaraunts__input"
          id="name"
          type="text"
          placeholder="NAME RESTAURANT"
        />
      </div>
      <div class="add-restaraunts__cell">
        <label class="add-restaraunts__subtitle" for="address">Адрес ресторана</label>
        <input
          v-model="restaurant.address"
          class="add-restaraunts__input"
          id="address"
          type="text"
          placeholder="2809 SPENARD RD"
        />
      </div>
      <div class="add-restaraunts__cell">
        <label class="add-restaraunts__subtitle" for="city">Город</label>
        <input
          v-model="restaurant.city"
          class="add-restaraunts__input"
          id="city"
          type="text"
          placeholder="FLORIDA"
        />
      </div>
      <div class="add-restaraunts__cell">
        <label class="add-restaraunts__subtitle" for="date">Дата инспекции</label>
        <input
          v-model="restaurant.date"
          class="add-restaraunts__input"
          id="date"
          type="text"
          placeholder="2014-12-29"
        />
      </div>
      <div class="add-restaraunts__cell">
        <label class="add-restaraunts__subtitle" for="status">Статус инспекции</label>
        <input
          v-model="restaurant.description"
          class="add-restaraunts__input"
          id="status"
          type="text"
          placeholder="NO ACTION"
        />
      </div>
    </div>
    <div class="add-restaraunts__buttons">
      <button class="add-restaraunts__button">Добавить!</button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'NewRestaurants',
  props: {
    restaurant: {
      type: Object,
      default: () => ([]),
    },
    messageValidation: {
      type: String,
      required: true,
    },
  },

  methods: {
    onSubmit() {
      this.$emit('onSubmit', this.restaurant);
    },
  },
};
</script>

<style lang="scss">
.add-restaraunts {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
  border: 1px solid #000;
  padding: 10px;
  row-gap: 20px;

  &__title {
    margin-bottom: 10px;
  }

  &__row {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }

  &__cell {
    display: flex;
    flex-direction: column;
    align-items: center;
    row-gap: 5px;
  }

  &__subtitle {
    letter-spacing: 1.2px;
    text-transform: uppercase;
  }

  &__input {
    padding: 8px;
    outline: none;
    border: 1px solid #999;
    transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);

    &:hover {
      border-color: #5b68b4;
    }

    &:focus {
      border-color: #34b485;
    }
  }

  &__buttons {
    margin: 0 auto;
  }

  &__button {
    font-weight: 700;
    letter-spacing: 1.1px;
    padding: 10px 20px;
    background-color: transparent;
    outline: none;
    border: 1px solid #999;
    transition: all 0.3s linear;
    cursor: pointer;

    &:hover {
      color: #fff;
      background-color: #5b68b4;
      border-color: #5b68b4;
    }

    &:focus {
      color: #fff;
      background-color: #34b485;
      border-color: #34b485;
    }
  }

  &__error {
    color: crimson;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1.2px;
    text-align: center;
    margin: 0;
  }
}
</style>
