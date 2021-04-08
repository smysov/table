<template>
  <ul class="edit-list">
    <li class="edit-list__item" v-for="field of fields" :key="field.key">
      <div class="edit-list__wrapper-icon">
        <img class="edit-list__cross" src="../assets/images/check.svg" alt="icon" />
      </div>
      <span class="edit-list__title">{{ field.name }}</span>
    </li>
    <!-- <li class="edit-list__item">
      <div class="edit-list__wrapper-icon">
        <img class="edit-list__cross" src="../assets/images/check.svg" alt="icon" />
      </div>
      <span class="edit-list__title">Адрес ресторана</span>
    </li>
    <li class="edit-list__item">
      <div class="edit-list__wrapper-icon">
        <img class="edit-list__cross" src="../assets/images/check.svg" alt="icon" />
      </div>
      <span class="edit-list__title">Город</span>
    </li>
    <li class="edit-list__item">
      <div class="edit-list__wrapper-icon">
        <img class="edit-list__cross" src="../assets/images/check.svg" alt="icon" />
      </div>
      <span class="edit-list__title">Номер ресторана</span>
    </li>
    <li class="edit-list__item">
      <div class="edit-list__wrapper-icon">
        <img class="edit-list__cross" src="../assets/images/check.svg" alt="icon" />
      </div>
      <span class="edit-list__title">Статус инспекции</span>
    </li>
    <li class="edit-list__item">
      <div class="edit-list__wrapper-icon">
        <img class="edit-list__cross" src="../assets/images/check.svg" alt="icon" />
      </div>
      <span class="edit-list__title">Дата инспекции</span>
    </li> -->
  </ul>
</template>

<script>
export default {
  name: 'EditList',
  props: {
    fields: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.edit-list {
  position: absolute;
  top: 38px;
  left: -1px;
  background-color: #fff;
  width: 338px;
  border: 1px solid #000;
  border-top: none;
  z-index: 100;

  &__item {
    display: flex;
    align-items: flex-end;
    padding: 10px 0 10px 6px;
    border-top: 1px solid #000;
  }

  &__wrapper-icon {
    margin-right: 5px;
  }

  &__cross {
    width: 33px;
    height: 25px;
  }

  &__title {
    font-size: 24px;
  }
}
</style>
