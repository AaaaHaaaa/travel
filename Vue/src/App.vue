<template>
  <div class="main">
    <el-container style="width: 100%; height: 100%">
      <el-aside>
        <Aside :talks="talks" />
      </el-aside>
      <el-container style="width: 75%; height: 100%">
        <el-main>Main</el-main>
        <el-footer>Footer</el-footer>
      </el-container>
    </el-container>
  </div>
</template>

<script setup>
import { ref, computed, reactive } from "vue";
import Aside from "./components/aside.vue";

const talks = reactive([
  { id: 1, name: "FirstTalk" },
  { id: 2, name: "SecondTalk" },
  { id: 3, name: "ThirdTalk" },
]);
</script>

<style scoped>
.main {
  position: absolute;
  width: 100%;
  height: 100%;
}
.el-aside {
  background-color: #eae9f4;
}
.el-main {
  height: 70%;
}
.el-footer {
  height: 30%;
}
</style>
