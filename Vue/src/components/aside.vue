<template>
  <div class="create">
    <div class="header">
      <el-button
        color="#626aef"
        @click="createTalks()"
        plain
        round
        class="create-button"
      >
        + 新建对话
      </el-button>
    </div>
    <div class="list">
      <h5 v-if="len == 0" class="no-data">暂无数据</h5>
      <ul class="talks-list">
        <li v-for="item in Toptalks" :key="item.id" class="talks-item">
          <div
            class="talks-view"
            @mouseenter="item.hover = true"
            @mouseleave="item.hover = false"
          >
            <el-button @click="currentTalks(item.id)" class="talks-button">
              <p v-if="!item.edit">{{ item.name }}</p>
              <input
                v-else
                v-model.trim="item.name"
                @keyup.enter="edit(item.id, item.name)"
                class="edit-input"
              />
            </el-button>
            <div class="action-buttons" v-if="item.hover">
              <button @click="isTopTalks(item.id)">取消置顶</button>
              <button @click="RenameTalks(item.id)">重命名</button>
              <button @click="deleteTalks(item.id)">删除</button>
            </div>
          </div>
        </li>
        <li v-for="item in talks" :key="item.id" class="talks-item">
          <div
            class="talks-view"
            @mouseenter="item.hover = true"
            @mouseleave="item.hover = false"
            v-if="item.isTop == false"
          >
            <el-button @click="currentTalks(item.id)" class="talks-button">
              <p v-if="!item.edit">{{ item.name }}</p>
              <input
                v-else
                v-model.trim="item.name"
                @keyup.enter="edit(item.id, item.name)"
                class="edit-input"
              />
            </el-button>
            <div class="action-buttons" v-if="item.hover">
              <button @click="isTopTalks(item.id)">置顶</button>
              <button @click="RenameTalks(item.id)">重命名</button>
              <button @click="deleteTalks(item.id)">删除</button>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, ref } from "vue";
const props = defineProps(["talks", "len", "Toptalks"]);

const emit = defineEmits([
  "createTalks",
  "deleteTalks",
  "isTopTalks",
  "RenameTalks",
  "currentTalks",
  "edit",
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
const RenameTalks = (talks_Id) => {
  emit("RenameTalks", talks_Id);
};
const edit = (talks_Id, rename) => {
  emit("edit", talks_Id, rename);
};
</script>

<style scoped>
.create {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

.header {
  margin-bottom: 20px;
}

.create-button {
  width: 180px;
  height: 50px;
  font-size: 16px;
}

.list {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
}

.no-data {
  text-align: center;
  color: #999;
  font-style: italic;
}

.talks-list {
  list-style: none;
  padding: 0;
}

.talks-item {
  margin: 10px 0;
}

.talks-view {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #e0e0e0;
  border-radius: 5px;
  background-color: #f9f9f9;
  position: relative;
}

.talks-button {
  flex: 1;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.edit-input {
  flex: 1;
  margin: 0 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 5px;
}

.action-buttons {
  display: flex;
  gap: 5px;
  position: absolute;
  right: 10px;
  visibility: hidden;
}

.talks-view:hover .action-buttons {
  visibility: visible;
}

button {
  background-color: #e0e0e0;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #d0d0d0;
}
</style>
