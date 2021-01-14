<template>
  <div class="card card-w70">
    <slot></slot>
    <h3 v-if="blocksCount === 0">
      Добавьте первый блок, чтобы увидеть результат
    </h3>
  </div>
</template>

<script>
export default {
  props: {
    blocksCount: {
      type: Number,
      default: 0
    }
  }
};
</script>

<style scoped></style>
