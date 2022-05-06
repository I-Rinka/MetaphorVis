<script setup>
import { computed, reactive, ref, toRaw } from "vue";
import { Content } from "../data/content";
import { Search, Aim } from "@element-plus/icons-vue";
import CardView from "./Card.vue";
import DetailView from "./DetailView.vue";

const data = reactive({
  content: [],
  filters: ["", "", ""],
  show_detail: false,
  current_content: null,
});

for (let i = 0; i < 10; i++) {
  data.content.push(
    new Content(
      `Wyx ${i}`,
      "A Very Decent Title",
      "/test.png",
      ["test1", "d3"],
      { author: "haha" }
    )
  );
}

for (let i = 0; i < 7; i++) {
  data.content.push(
    new Content(
      `Wzc ${i}`,
      "A Very Decent Title2",
      "/test2.png",
      ["test2", "d3"],
      {
        author: "WZC",
      }
    )
  );
}

for (let i = 11; i < 13; i++) {
  data.content.push(
    new Content(
      `Wyx ${i}`,
      "A Very Decent Title",
      "/test.png",
      ["test1", "d4"],
      { author: "haha" }
    )
  );
}

const show_cards = computed(() => {
  if (data.filters.join("") === "") {
    return data.content;
  } else {
    console.log(data.filters);
    return data.content.filter((d) => {
      for (let i = 0; i < data.filters.length; i++) {
        const filter = data.filters[i];
        if (filter !== "") {
          if (d.group.find((d) => d === filter) === undefined) {
            return false;
          }
        }
      }
      return true;
    });
  }
});

function Filter(filter_index, condition) {
  data.filters[filter_index] = condition;
}

function ShowDetailWindow(content) {
  data.show_detail = true;
  data.current_content = content;
}
</script>

<template>
  <div class="index">
    <div class="header">
      <div class="title-row"><div>Metaphor Vis</div></div>
      <div class="function-row">
        <div class="function-group">
          <div>Dimensionality</div>
          <el-button
            color="rgb(72, 124, 198)"
            type="primary"
            @click="Filter(0, '')"
          >
            <el-icon color="white"><aim /></el-icon>
          </el-button>

          <el-button
            color="rgb(72, 124, 198)"
            type="primary"
            @click="Filter(0, 'test1')"
          >
            <el-icon color="white"><aim /></el-icon>
          </el-button>

          <el-button
            color="rgb(72, 124, 198)"
            type="primary"
            @click="Filter(0, 'test2')"
          >
            <el-icon color="white"><aim /></el-icon>
          </el-button>
        </div>

        <div class="function-group">
          <div>Representation</div>
          <el-button
            color="rgb(72, 124, 198)"
            type="primary"
            @click="Filter(1, '')"
          >
            <el-icon color="white"><aim /></el-icon>
          </el-button>
          <el-button
            color="rgb(72, 124, 198)"
            type="primary"
            @click="Filter(1, 'd3')"
          >
            <el-icon color="white"><aim /></el-icon>
          </el-button>
        </div>

        <div class="function-group"><div>Alignment</div></div>

        <div class="function-group">
          <div>Fulltext Search</div>
          <el-input clearable :suffix-icon="Search" size="small"></el-input>
        </div>

        <div class="function-group">
          <div>Techniques Shown</div>
          <div
            style="
              margin-top: -10px;
              font-size: 35px;
              font-weight: bolder;
              text-align: center;
            "
          >
            {{ show_cards.length }}
          </div>
        </div>
      </div>
    </div>

    <div class="content">
      <div class="gallery">
        <div v-for="c in show_cards" :key="c.id">
          <card-view @clickCard="ShowDetailWindow" :content="c"></card-view>
        </div>
      </div>
    </div>

    <div v-if="data.show_detail">
      <detail-view
        @close="data.show_detail = false"
        :content="data.current_content"
      ></detail-view>
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
      height: 60px;
      padding: 10px 20px 10px 10px;
      font-size: 40px;
      font-weight: bolder;
      color: white;
      display: flex;
      justify-content: center;
    }

    .function-row {
      width: 100%;
      height: 95px;
      background-color: rgb(203, 225, 252);
      border-bottom: solid 2px rgb(96, 98, 102);
      display: flex;
      justify-content: center;

      .function-group {
        font-size: 18px;
        margin: 10px 20px 10px 20px;
        text-align: center;
        div {
          margin-bottom: 10px;
        }
      }
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
