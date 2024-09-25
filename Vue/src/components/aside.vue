<template>
  <div class="create">
    <div>
      <el-button
        color="#626aef"
        :dark="isDark"
        @click="createTalks()"
        plain
        round
        style="width: 180px; height: 50px"
      >
        + 新建对话
      </el-button>
    </div>
    <div class="list">
      <h5 v-if="len == 0">暂无数据</h5>
      <ul class="talks-list">
        <li v-for="item in Toptalks" :key="item.id" class="Toptalks">
          <div class="talks-view">
            <el-button @click="currentTalks(item.id)"
              >{{ item.name }}
              <button @click="isTopTalks(item.id)">取消置顶</button>
              <button @click="RenameTalks(item.id)">重命名</button>
              <button @click="deleteTalks(item.id)">删除</button></el-button
            >
          </div>
        </li>
        <li v-for="item in talks" :key="item.id" class="talks">
          <div class="talks-view" v-if="item.isTop == false">
            <el-button @click="currentTalks(item.id)"
              >{{ item.name }}<button @click="isTopTalks(item.id)">置顶</button>
              <button @click="RenameTalks(item.id)">重命名</button>
              <button @click="deleteTalks(item.id)">删除</button></el-button
            >
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script  setup>
import { defineProps, defineEmits } from "vue";
const props = defineProps(["talks", "len", "Toptalks"]);

const emit = defineEmits([
  "createTalks",
  "deleteTalks",
  "isTopTalks",
  "RenameTalks",
  "currentTalks",
]);

const createTalks = () => {
  emit("createTalks");
};
const currentTalks = (talks_Id) => {
  emit("currentTalks", talks_Id);
};
const deleteTalks = (talks_Id) => {
  emit("deleteTalks", talks_Id);
};
const isTopTalks = (talks_Id) => {
  emit("isTopTalks", talks_Id);
};
const RenameTalks = (talks_Id) => {};
</script>

<style scoped>
.create {
  display: grid;
  justify-content: center;
  align-items: center;
  margin-top: 50px;
  grid-template-rows: 1fr auto;
}
.list {
  margin: 0 auto;
  margin-top: 50px;
}
</style>
