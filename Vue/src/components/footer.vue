<template>
  <input
    type="text"
    placeholder="通过shift+回车换行"
    v-model.trim="MyRequest"
    @keyup.enter="Request()"
  />
</template>

<script  setup>
import { ref } from "vue";
const MyRequest = ref("");
const emit = defineEmits(["addTalks"]);

const Request = () => {
  if (MyRequest.value.trim() === "") {
    ElMessage('请输入内容')
    return;
  }
  else {
    emit("addTalks",MyRequest.value)
    MyRequest.value = "";
  }
};
</script>

<style scoped>
</style>
