<template>
  <div class="input-container">
    <textarea
      type="text"
      placeholder="通过shift+回车换行"
      v-model.trim="MyRequest"
      @keyup.enter="Request()"
    ></textarea>
  </div>
</template>

<script  setup>
import { ref } from "vue";
const MyRequest = ref("");
const emit = defineEmits(["addTalks"]);

const Request = () => {
  if (MyRequest.value.trim() === "") {
    ElMessage("请输入内容");
    return;
  } else {
    emit("addTalks", MyRequest.value);
    MyRequest.value = "";
  }
};
</script>

<style scoped>
.input-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

textarea {
  width: 100%;
  max-width: 800px;
  min-height: 100px;
  padding: 15px;
  font-size: 18px;
  border: 2px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: border-color 0.3s;
  resize: vertical;
}

textarea:focus {
  border-color: #007bff;
  outline: none;
}
</style>
