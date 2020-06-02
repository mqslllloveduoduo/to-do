<template>
  <div>
    <h2>Add To-Do</h2>
    <!-- 捕获子组件发给父组件的事件：方法如果不写参数，默认是传递了所有的参数 -->
    <ToDoDetail @toDoAdd_Parent="toDoAdd_Parent" @modifyToDo_Parent="modifyToDo_Parent"></ToDoDetail>
  </div>
</template>

<script>
import ToDoDetail from "../components/To-do-detail";

export default {
  components: {
    ToDoDetail
  },
  data() {
    return {};
  },
  methods: {
    toDoAdd_Parent(toDo) {
      // 调用vuex中的方法，并传递参数
      this.$store.commit("toDoAdd", toDo);
      // 编程式路由，直接跳回到home页
      this.$router.push("/");
    },
    modifyToDo_Parent(modifiedToDo) {
      this.$store.commit("toDoModify", modifiedToDo);
      this.$router.push("/");
    }
  }
};
</script>

<style>
.space {
  padding: 10px;
}
.el-input {
  line-height: 100%;
}
.el-input-title {
  padding: 10px 0;
  float: left;
}
.el-date-editor.el-input,
.el-date-editor.el-input__inner {
  width: 100% !important;
}
.el-button {
  width: 100% !important;
}
</style>