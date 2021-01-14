<template>
  <div class="select" :class="{ open: isOpen }">
    <div class="select__backdrop" @click="close"></div>
    <div class="select__input" @click="toggle">
      <span class="select__value">{{ current.name }}</span>
      <i class="triangle"></i>
    </div>
    <div class="select__dropdown">
      <ul class="select__list">
        <li
          :key="item.id"
          v-for="item in items"
          class="select__item"
          :class="{ selected: current.id === item.id }"
          @click="select(item.id)"
        >
          {{ item.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['update:modelValue'],
  props: {
    modelValue: String,
    items: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      isOpen: false
    };
  },
  methods: {
    select(id) {
      this.$emit('update:modelValue', id);
      this.close();
    },
    toggle() {
      this.isOpen ? this.close() : this.open();
    },
    open() {
      this.isOpen = true;
    },
    close() {
      this.isOpen = false;
    }
  },
  computed: {
    current() {
      return this.items.find(item => item.id === this.modelValue);
    }
  }
};
</script>

<style lang="scss" scoped>
$height: 34px;
$white: #fff;
$grey: #ccc;

* {
  box-sizing: border-box;
}

.select {
  width: 100%;
  position: relative;
  z-index: 100;
  &__value {
    display: block;
    width: 100%;
  }
  &__backdrop {
    display: none;
    z-index: -1;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
  }
  &.open {
    .select__dropdown {
      display: block;
    }
    .select__backdrop {
      display: block;
    }
    .triangle {
      border-top: 5px solid transparent;
      border-bottom: 5px solid #000;
      transform: translateY(-75%);
    }
  }
  &__input {
    height: $height;
    position: relative;
    border-radius: 5px;
    border: 1px solid $grey;
    padding: 5px 30px 5px 1.5rem;
    background-color: $white;
    color: #000;
    font-size: 0.875rem;
    font-weight: 500;
    letter-spacing: 0.9px;
    width: 100%;
    outline: none;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  &__dropdown {
    display: none;
    position: absolute;
    z-index: 10;
    border: 1px solid $grey;
    background-color: $white;
    border-radius: 5px;
    top: $height;
    left: 0;
    right: 0;
    max-height: 200px;
    overflow-y: auto;
    margin-top: -1px;
  }
  &__list {
    padding: 0;
    margin: 0;
    list-style: none;
  }

  &__item {
    padding: 7px 10px;
    font-size: 0.875rem;
    font-weight: 400;
    letter-spacing: 0.9px;
    position: relative;
    transition: 0.15s background-color ease-in;
    &.selected {
      background-color: #eee;
    }
    &:hover {
      background-color: #ddd;
      cursor: pointer;
    }
  }
}
.triangle {
  position: absolute;
  top: 50%;
  right: 10px;
  display: inline-block;
  width: 0;
  height: 0;
  border-top: 5px solid #000;
  border-right: 5px solid transparent;
  border-bottom: 5px solid transparent;
  border-left: 5px solid transparent;
  transform: translateY(-25%);
}
</style>
