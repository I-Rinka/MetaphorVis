<script setup>
import { reactive, ref } from "vue";
import { Content } from "../data/content";
import CardView from "./Card.vue";

const data = reactive({
  content: [],
});

for (let i = 0; i < 10; i++) {
  data.content.push(
    new Content(
      `Wyx ${i}`,
      "Very Decent Title",
      "/test.png",
      ["test1", "test2"],
      { author: "haha" }
    )
  );
}
</script>

<template>
  <div class="index">
    <div class="header">
      <div class="title-row">Metaphor Vis</div>
      <div class="function-row"></div>
    </div>

    <div class="content">
      <div class="gallery">
        <div v-for="c in data.content" :key="c.id">
          <card-view :content="c"></card-view>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="less" scoped>
.index {
  height: 100vh;
  .header {
    position: fixed;
    z-index: 10;
    top: 0;
    width: 100%;
    .title-row {
      background-color: rgb(72, 124, 198);
      padding: 10px 20px 10px 10px;
      font-size: 40px;
      font-weight: bolder;
      color: white;
    }

    .function-row {
      width: 100%;
      height: 100px;
      background-color: rgb(170, 206, 251);
    }
  }

  .content {
    position: absolute;
    top: 175px;
    width: 100%;

    .gallery {
      padding: 10px 30px 10px 30px;
      display: flex;
      justify-content: left;
      flex-wrap: wrap;
    }
  }
}
</style>
