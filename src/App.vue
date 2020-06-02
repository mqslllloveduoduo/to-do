<template>
  <div>
    <el-container>
      <el-header>
        <div style="font-size: 20px;">您好，XXX！</div>
        <el-menu active-text-color="#E6A23C" mode="horizontal">
          <el-menu-item index="1">
            <router-link to="/">Home</router-link>
          </el-menu-item>
          <el-menu-item index="2">
            <router-link to="/toDo">Add To-Do</router-link>
          </el-menu-item>
        </el-menu>
      </el-header>
      <el-main height="100px">
        <!-- 通过key值的变化去强制刷新后面的To-do-detail组件，刷新一次即可，因为一次以后路径和query就不再变化，也符合需求。 -->
        <router-view :key="$route.path + $route.query.action"></router-view>
      </el-main>
    </el-container>
  </div>
</template>

<script>
export default {};
</script>

<style>
body {
  margin: 0;
}
.el-menu--horizontal > .el-menu-item.is-active {
  border-bottom: 0 !important;
}
.el-header {
  padding: 0 !important;
  position: fixed;
  width: 100%;
  z-index: 1001;
}
.el-menu-item {
  padding: 0 !important;
  transition: none !important;
}
.el-header,
.el-footer {
  background-color: #409eff;
  color: #333;
  text-align: center;
  line-height: 50px;
  height: 50px !important;
}
.el-main {
  /* background-color: #e9eef3; */
  color: #333;
  text-align: center;
  line-height: 100px;
  top: 100px;
  position: relative;
  z-index: 1000;
  padding: 0 20px !important;
}
body > .el-container {
  margin-bottom: 40px;
}
li.el-menu-item {
  width: 50%;
}
li a {
  text-decoration: none;
  font-size: 20px;
}
.el-menu-item.is-active {
  color: white;
}
.el-menu--horizontal > .el-menu-item {
  border-bottom: none !important;
}
</style>