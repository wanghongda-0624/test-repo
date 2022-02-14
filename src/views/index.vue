<template>
  <!-- <el-container class="index-con">
    <el-header class="index-header">
      <navcon></navcon>
    </el-header>
    <el-container class="index-con">
      <el-aside :class="showclass">
        <leftnav></leftnav>
      </el-aside>
      <el-container class="main-con">
        <el-main clss="index-main">
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </el-container> -->

  <el-container class="index-con">
    <el-aside :class="showclass" style="width: 240px">
      <leftnav></leftnav>
    </el-aside>
    <el-aside v-if= "chart = false" class="showclass2">
      <rightnav></rightnav>
    </el-aside>
    <el-container class="main-con">
      <el-header class="index-header">
        <navcon></navcon>
      </el-header>
      <el-main clss="index-main">
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>
<script>
// 导入组件
import navcon from '../components/navcon.vue'
import leftnav from '../components/leftnav.vue'
import rightnav from '../components/rightnav.vue'
export default {
  name: 'index',
  data() {
    return {
      showclass: 'asideshow',
      showtype: false,
      chart: this.$store.state.showright
    }
  },
  // 注册组件
  components: {
    navcon,
    leftnav,
    rightnav
  },
  methods: {},
  created() {
    // 监听
    this.$root.Bus.$on('toggle', value => {
      if (value) {
        this.showclass = 'asideshow'
      } else {
        setTimeout(() => {
          this.showclass = 'aside'
        }, 300)
      }
    })
  },
  beforeUpdate() {},
  // 挂载前状态(里面是操作)
  beforeMount() {
    // 弹出登录成功
    this.$message({
      message: '登录成功',
      type: 'success'
    })
  }
}
</script>
<style >
.index-con {
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}

.aside {
  width: 64px !important;
  height: 100%;
  background-color: #fff;
  margin: 0px;
}
.asideshow {
  width: 240px !important;
  height: 100%;
  background-color: #fff;
  margin: 0px;
}
.showclass2 {
  width: 160px !important;
  height: 100%;
  background-color: #fff;
  margin: 0px;
  position: absolute;
  left:86%;
}
.index-header,
.index-main {
  padding: 0px;
  border-left: 0px solid #333;
  
}
.el-main{
  background-color: #EDEDED;
}
</style>
