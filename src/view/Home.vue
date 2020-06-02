<template>
  <div>
    <h2>To-Do list...</h2>
    <el-row>
      <el-col class="todo-item" :span="24" v-for="(todo, index) in toDos" :key="index">
        <ToDoItem :data="todo"></ToDoItem>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from "axios";
import ToDoItem from "../components/To-do-item";
import { mapGetters } from "vuex";

export default {
  computed: {
    // mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性，省去了this.$store.getters.allToDos这样的写法
    ...mapGetters({
      allToDos: "allToDos"
    }),
    toDoList: {
      get() {
        // 第一次this.allToDos也为空
        // console.log(345678);
        // console.log(this.allToDos);
        // this.toDoList直接引用了store里的allToDos
        return this.allToDos;
      },
      set(newVal) {
        // 当发生（数据）变化时。。。
        this.$store.commit("updateAllToDos", newVal);
      }
    }
  },
  components: {
    ToDoItem
  },
  data() {
    return {
      toDos: []
    };
  },
  async created() {
    if (this.toDoList && this.toDoList.length > 0) {
      this.toDos = this.toDoList;
    } else {
      let result = await axios.get("/api/toDos");
      this.toDos = result.data.data;
      // 触发了toDoList的set方法
      this.toDoList = this.toDos;
    }
  }
};
</script>

<style>
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.max-row-height {
  line-height: 50px;
}
.todo-item {
  background: rgba(0, 0, 0, 0.04);
  border-color: orchid;
  margin: 10px 0 10px 0;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}
</style>