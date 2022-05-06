<script setup>
import { Content } from "../data/content";
const props = defineProps({
  content: {
    type: Content,
  },
});
</script>
<template>
  <div class="card">
    <el-image class="preview-img" :src="props.content.picture" fit="cover" />
  </div>
</template>
<style lang="less" scoped>
.card {
  margin: 15px;
  background-color: white;
  border-radius: 5px;
  cursor: pointer;
  filter: drop-shadow(2px 2px 5px rgba(0, 0, 0, 0.5));
  height: 130px;
  width: 130px;

  transition: 0.5s;
  &:hover {
    transform: scale(1.2, 1.2);
  }
}
.preview-img {
  margin: 5px;
  height: 120px;
  width: 120px;
}
</style>

