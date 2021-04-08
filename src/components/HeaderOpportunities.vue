<template>
  <div class="header-table">
    <h2 class="header-table__title"> Инспекция по ресторанам </h2>
    <div class="button-wrapper">
      <button class="header-table__edit" @click="onShowParameters">
        Редактировать таблицу
      </button>
      <transition name="opacity">
        <edit-list v-show="isShowParameters" :fields="fields"/>
      </transition>
    </div>
    <input
      class="header-table__search"
      type="text"
      placeholder="Поиск по полям таблицы"
      v-model="search"
    />
  </div>
</template>

<script>
import EditList from '@/components/EditList.vue';

export default {
  name: 'Header',
  props: {
    isShowParameters: {
      type: Boolean,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
    fields: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      search: this.value,
    };
  },
  components: {
    EditList,
  },

  methods: {
    onShowParameters() {
      this.$emit('onShowParameters');
    },
  },
  watch: {
    search(value) {
      this.$emit('search', value);
    },
  },
};
</script>

<style lang="scss">
.button-wrapper {
  position: relative;
}

.header-table {
  display: flex;
  align-items: center;
  justify-content: space-between;

  &__title {
    padding: 28px 114px 28px 63px;
  }

  &__edit {
    font-size: 18px;
    background-color: transparent;
    border: 1px solid #999;
    padding: 8px 47px 9px;
    width: 335px;
    transition: all 0.3s cubic-bezier(0.23, 1, 0.32, 1);
    outline: none;
    cursor: pointer;

    &:hover {
      color: #fff;
      border-color: #5b68b4;
      background-color: #5b68b4;
    }

    &:focus {
      color: #fff;
      border-color: #34b485;
      background-color: #34b485;
    }
  }

  &__search {
    padding: 8px 174px 8px 16px;
    margin: 18px 43px 18px 33px;
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
}

.opacity-enter-active {
  transition: all 0.3s linear;
}
.opacity-leave-active {
  transition: all 0.3s linear;
}
.opacity-enter,
.opacity-leave-to {
  transform: translateY(25px);
  opacity: 0;
}
</style>
