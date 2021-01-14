<template>
  <div class="card">
    <h2>Комментарии</h2>
    <ul class="list">
      <Comment
        :key="comment.id"
        v-for="comment in comments"
        :comment="comment"
      />
    </ul>
  </div>
</template>

<script>
import Comment from './Comment';
export default {
  props: ['comments'],
  components: {
    Comment
  }
};
</script>

<style scoped></style>
