<template>
  <div class="main">
    <el-container style="width: 100%; height: 100%">
      <el-aside>
        <Aside
          :talks="talks"
          :len="len"
          :Toptalks="Toptalks"
          @createTalks="createTalks"
          @currentTalks="currentTalks"
          @deleteTalks="deleteTalks"
          @isTopTalks="isTopTalks"
          @RenameTalks="RenameTalks"
          @edit="edit"
        />
      </el-aside>
      <el-container style="width: 75%; height: 100%">
        <el-main><Main :talks="current" /></el-main>
        <el-footer><Footer @addTalks="addTalks" /></el-footer>
      </el-container>
    </el-container>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { ElMessage } from "element-plus";
import Aside from "./components/aside.vue";
import Main from "./components/main.vue";
import Footer from "./components/footer.vue";

const talks = ref([
  {
    id: 1,
    name: "FirstTalk",
    dialogue: [
      { id: 1, request: "你好", response: "你好,我是AI！有什么可以帮你的吗？" },
    ],
    isTop: false,
    edit: false,
  },
  {
    id: 2,
    name: "SecondTalk",
    dialogue: [{ id: 1, request: "你是谁", response: "我是AI！" }],
    isTop: false,
    edit: false,
  },
  {
    id: 3,
    name: "ThirdTalk",
    dialogue: [{ id: 1, request: "芜湖", response: "我不明白你在说什么" }],
    isTop: false,
    edit: false,
  },
]);
const current = ref({
  id: 0,
  name: "",
  dialogue: [],
  isTop: false,
  edit: false,
});
const Toptalks = computed(() => talks.value.filter((talks) => talks.isTop));

const createTalks = () => {
  if (current.value.id == 0) {
    ElMessage("已是最新对话！");
  } else {
    current.value = {
      id: 0,
      name: "",
      dialogue: [],
      isTop: false,
      edit: false,
    };
  }
};
const currentTalks = (talks_Id) => {
  const index = talks.value.findIndex((item) => item.id == talks_Id);
  current.value = talks.value[index];
};
const deleteTalks = (talks_Id) => {
  if (current.value.id == talks_Id) {
    current.value = {
      id: 0,
      name: "",
      dialogue: [],
      isTop: false,
      edit: false,
    };
  }
  talks.value = talks.value.filter((talks) => talks.id !== talks_Id);
  if (talks.value.length == 0) {
    current.value = {
      id: 0,
      name: "",
      dialogue: [],
      isTop: false,
      edit: false,
    };
  }
};
const isTopTalks = (talks_Id) => {
  const index = talks.value.findIndex((item) => item.id == talks_Id);
  talks.value[index].isTop = !talks.value[index].isTop;
};
const RenameTalks = (talks_Id) => {
  const index = talks.value.findIndex((item) => item.id == talks_Id);
  talks.value[index].edit = !talks.value[index].edit;
};
const edit = (talks_Id, rename) => {
  if (rename == "") {
    ElMessage("请输入对话名称！");
    return;
  }
  const index = talks.value.findIndex((item) => item.id == talks_Id);
  talks.value[index].name = rename;
  talks.value[index].edit = !talks.value[index].edit;
};
const len = computed(() => talks.value.length);

const ai_response = (Request) => {
  if (Request == "你好") {
    return "你好,我是AI！有什么可以帮你的吗？";
  } else if (Request == "你是谁") {
    return "我是AI！";
  } else {
    return "对不起,我不明白你在说什么";
  }
};
const addTalks = (MyRequest) => {
  var response = ai_response(MyRequest);
  if (talks.value.length == 0) {
    talks.value.push({
      id: 1,
      name: MyRequest,
      dialogue: [{ id: 1, request: MyRequest, response: response }],
      isTop: false,
      edit: false,
    });
    current.value = talks.value[0];
  } else if (current.value.id == 0) {
    talks.value.push({
      id: talks.value[talks.value.length - 1].id + 1,
      name: MyRequest,
      dialogue: [{ id: 1, request: MyRequest, response: response }],
      isTop: false,
      edit: false,
    });
    current.value = talks.value[talks.value.length - 1];
  } else {
    const index = talks.value.findIndex(
      (talks) => talks.id == current.value.id
    );
    talks.value[index].dialogue.push({
      id: talks.value[index].dialogue.length + 1,
      request: MyRequest,
      response: response,
    });
    current.value = talks.value[index];
  }
};
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
