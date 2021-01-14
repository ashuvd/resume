<template>
  <form class="card card-w30" @submit.prevent="submitHandler">
    <div class="form-control">
      <label>Тип блока</label>
      <Select v-model="selectItem" :items="selectItems" />
    </div>
    <div class="form-control">
      <label for="value">Значение</label>
      <textarea v-model.trim="value" id="value" rows="3"></textarea>
    </div>
    <button class="btn primary" :disabled="isButtonDisabled">Добавить</button>
  </form>
</template>

<script>
import Select from '@/components/plugins/Select';
export default {
  emits: ['add'],
  data() {
    return {
      selectItem: 'title',
      value: '',
      selectItems: [
        {
          id: 'title',
          name: 'Заголовок'
        },
        {
          id: 'subtitle',
          name: 'Подзаголовок'
        },
        {
          id: 'avatar',
          name: 'Аватар'
        },
        {
          id: 'text',
          name: 'Текст'
        }
      ]
    };
  },
  computed: {
    isButtonDisabled() {
      return this.value.length <= 3;
    }
  },
  methods: {
    submitHandler() {
      this.$emit('add', {
        type: this.selectItem,
        payload: this.value
      });
      this.selectItem = 'title';
      this.value = '';
    }
  },
  components: {
    Select
  }
};
</script>

<style scoped></style>
