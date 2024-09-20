<template>
  <div class="create">
    <div>
      <el-button
        color="#626aef"
        :dark="isDark"
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
        <li v-for="item in talks" :key="item.id">
          <el-button class="talks-view">
            <p>{{ item.name }}</p>

            <button @click="deleteTalks(item.id)"></button>
          </el-button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script  setup>
import { defineProps, defineEmits } from "vue";
const props = defineProps(["talks", "len"]);
const emit = defineEmits(["deleteTalks"]);

const deleteTalks = (talks_Id) => {
  talks_Id && emit("deleteTalks", talks_Id);
};
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
.ul {
}
</style>
