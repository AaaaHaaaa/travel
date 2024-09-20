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
      <h5 v-if="talks == {}">暂无数据</h5>
      <ul class="talks-list">
        <li v-for="item in talks" :key="item.id">
          <div class="talks-view">
            <p>{{ item.name }}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script  setup>
const talks = defineProps(["talks"]);
console.log(talks.value);
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
