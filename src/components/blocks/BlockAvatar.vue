<template>
  <div class="avatar">
    <img :src="value" alt="img" />
  </div>
</template>

<script>
export default {
  props: ['value']
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
