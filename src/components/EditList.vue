<template>
  <ul class="edit-list">
    <li
      class="edit-list__item"
      v-for="field of fields"
      :key="field.key"
      @click="hideShowCell(field.key)"
    >
      <div class="edit-list__wrapper-icon">
        <img
          class="edit-list__check"
          src="../assets/images/check.svg"
          alt="icon"
          v-if="field.visible"
        />
        <img
          class="edit-list__cross"
          src="../assets/images/cross-hide.svg"
          alt="icon"
          v-else
        />
      </div>
      <span class="edit-list__title">{{ field.name }}</span>
    </li>
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
  methods: {
    hideShowCell(key) {
      this.$emit('hideShowCell', key);
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
    cursor: pointer;
    user-select: none;
  }

  &__wrapper-icon {
    margin-right: 5px;
  }

  &__check {
    width: 33px;
    height: 25px;
  }

  &__cross {
    width: 26px;
    height: 26px;
  }

  &__title {
    font-size: 24px;
  }
}
</style>
