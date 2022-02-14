/**
* 左边菜单
*/ 
<template>
  <el-menu
    :collapse="collapsed"
    collapse-transition
    router
    :default-active="$route.path"
    unique-opened
    class="el-menu-vertical-demo"
    background-color="#fff"
    text-color="#000"
    active-text-color="#E0301E"
  >
    <div class="logobox">
      <img class="logoimg" src="../assets/img/pwc.svg" alt="" />
      <el-button class="cloudhub" type="text">CloudHub</el-button>
    </div>
    <!-- <el-submenu v-for="menu in allmenu" :key="menu.menuid" :index="menu.menuname">
      <template slot="title">
        <i class="iconfont" :class="menu.icon"></i>
        <span>{{menu.menuname}}</span>
      </template>
      <el-menu-item-group>
        <el-menu-item v-for="chmenu in menu.menus" :index="'/'+chmenu.url" :key="chmenu.menuid">
          <i class="iconfont" :class="chmenu.icon"></i>
          <span>{{chmenu.menuname}}</span>
        </el-menu-item>
      </el-menu-item-group>
    </el-submenu> -->
    <p class="p1">Start Date</p>
    <el-select placeholder="please select your LoS">
      <el-option label="Assurance" value="shanghai"></el-option>
      <el-option label="Advisory" value="beijing"></el-option>
      <el-option label="Tax" value="shanghai"></el-option>
      <el-option label="OFS" value="beijing"></el-option>
      <el-option label="FCS" value="beijing"></el-option>
    </el-select>
    <p class="p1">End Date</p>
    <el-select placeholder="please select your LoS">
      <el-option label="Assurance" value="shanghai"></el-option>
      <el-option label="Advisory" value="beijing"></el-option>
      <el-option label="Tax" value="shanghai"></el-option>
      <el-option label="OFS" value="beijing"></el-option>
      <el-option label="FCS" value="beijing"></el-option>
    </el-select>
    <p class="p1">Category</p>
    <el-radio-group v-model="radio">
      <el-radio :label="3" class="r1">Option A</el-radio>
      <el-radio :label="6" class="r1">Option B</el-radio>
      <el-radio :label="9" class="r1">Option C</el-radio>
    </el-radio-group>
  </el-menu>
</template>
<script>
import { menu } from "../api/userMG";
export default {
  name: "rightnav",
  data() {
    return {
      collapsed: false,
      allmenu: [],
      radio: 3
    };
  },
  // 创建完毕状态(里面是操作)
  created() {
    // 获取图形验证码
    let res = {
      success: true,
      data: [],
      msg: "success",
    };
    this.allmenu = res.data;

    // menu(localStorage.getItem('logintoken'))
    //   .then(res => {
    //     console.log(JSON.stringify(res))
    //     if (res.success) {
    //       this.allmenu = res.data
    //     } else {
    //       this.$message.error(res.msg)
    //       return false
    //     }
    //   })
    //   .catch(err => {
    //     this.$message.error('菜单加载失败，请稍后再试！')
    //   })
    // 监听
    this.$root.Bus.$on("toggle", (value) => {
      this.collapsed = !value;
    });
  },
};
</script>
<style scoped>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 160px;
  min-height: 400px;
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
  border: none;
  text-align: left;
}
.el-menu-item-group__title {
  padding: 0px;
}
.el-menu-bg {
  background-color: #1f2d3d !important;
}
.el-menu {
  border: none;
}
.logobox {
  /* height: 40px;
  line-height: 40px;
  color: #9d9d9d;
  font-size: 20px;
  text-align: left;
  margin-left: 30px;
  padding: 20px 0px; */
}
.logoimg {
  height: 30px;
}
.cloudhub.el-button--text {
  color: #000;
}
el-menu-item is-active {
  color: #000;
}
.p1 {
  margin-left: 10px;
}
.r1{
    margin-top: 15px;
    margin-left: 10px;
}
</style>