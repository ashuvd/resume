<template>
  <div class="container column">
    <AppAddBlock @add="addBlock" />
    <AppContent :blocksCount="blocks.length">
      <component
        :key="i"
        v-for="(block, i) in blocks"
        :is="block.name"
        :value="block.value"
      />
    </AppContent>
  </div>
  <div class="container">
    <AppAddComment @load="fetchComments" />
    <AppComments v-if="comments.length && !loading" :comments="comments" />
    <AppLoader v-if="loading" />
  </div>
</template>

<script>
import AppLoader from './components/AppLoader';
import AppAddBlock from './components/AppAddBlock';
import AppContent from './components/AppContent';
import AppComments from './components/AppComments';
import AppAddComment from './components/AppAddComment';

import BlockTitle from './components/blocks/BlockTitle';
import BlockSubtitle from './components/blocks/BlockSubtitle';
import BlockAvatar from './components/blocks/BlockAvatar';
import BlockText from './components/blocks/BlockText';

export default {
  data() {
    return {
      blocks: [],
      comments: [],
      loading: false
    };
  },
  methods: {
    addBlock(action) {
      this.blocks.push({
        name: `block-${action.type}`,
        value: action.payload
      });
    },
    async fetchComments() {
      this.loading = true;
      const response = await fetch(
        'https://jsonplaceholder.typicode.com/comments?_limit=42'
      );
      this.comments = await response.json();
      console.log(this.comments)
      this.loading = false;
    }
  },
  components: {
    AppLoader,
    AppAddBlock,
    AppContent,
    AppComments,
    BlockTitle,
    BlockSubtitle,
    BlockAvatar,
    BlockText,
    AppAddComment
  }
};
</script>

<style></style>
