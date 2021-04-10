<template>
  <div class="modal"
    @click="onHideModal">
    <div class="modal__content"
      @click.stop="">
      <h2 class="modal__title"> Должен быть минимум один столбец! </h2>
      <button class="modal__button"
        @click="onHideModal">Ок</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalWarning',
  methods: {
    onHideModal() {
      this.$emit('onHideModal');
    },
  },
};
</script>

<style lang="scss">
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);

  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    row-gap: 20px;
    padding: 20px;
    background-color: #fff;
    border-radius: 10px;
  }

  &__button {
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1.1px;
    padding: 10px 20px;
    background-color: transparent;
    border: 1px solid #999;
    border-radius: 5px;
    cursor: pointer;
    outline: none;
    transition: all 0.3s ease-out;

    &:hover {
      color: #fff;
      border-color: #3291ac;
      background-color: #3291ac;
    }

    &:focus {
      color: #fff;
      border-color: #125568;
      background-color: #125568;
    }
  }
}
</style>
