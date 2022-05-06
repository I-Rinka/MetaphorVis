<script setup>
import { ref } from "vue";
import { data } from "../data/content";
</script>

<template>
  <div>
    <el-container>
      <el-header height="80px"
        ><div class="title-row">Metaphor Vis</div>
        <div class="function-row"></div
      ></el-header>
      <el-main>
        <div style="height: 100000px"></div>
      </el-main>
    </el-container>
  </div>
</template>

<style lang="less" scoped>
.el-header {
  background-color: rgb(72, 124, 198);
  position: fixed;
  width: 100%;

  .title-row {
    padding: 10px;
    font-size: 40px;
    font-weight: bolder;
    color: white;
  }

  .funciton-row {
    height: 100px;
    background-color: rgb(170, 206, 251);
  }
}
</style>
