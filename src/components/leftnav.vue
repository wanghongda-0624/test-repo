/**
* 左边菜单
*/ 
<template>
  <el-menu  :collapse="collapsed" collapse-transition router :default-active="$route.path" unique-opened class="el-menu-vertical-demo" background-color="#fff" text-color="#000" active-text-color="#E0301E">
    <div class="logobox">
      <img class="logoimg" src="../assets/img/pwc.svg" alt="">
      <el-button class="cloudhub" type="text" @click="backhome()">CloudHub</el-button>
    </div>
    <el-submenu v-for="menu in allmenu" :key="menu.menuid" :index="menu.menuname">
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
    </el-submenu>
  </el-menu>
</template>
<script>
import { menu } from '../api/userMG'
export default {
  name: 'leftnav',
  data() {
    return {
      collapsed: false,
      allmenu: []
    }
  },
  // 创建完毕状态(里面是操作)
  created() {
    // 获取图形验证码
    let res = {
      success: true,
      data: [
        {
          menuid: 1,
          icon: 'li-icon-xiangmuguanli',
          menuname: 'Cloud Resource',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 3,
              icon: 'icon-cat-skuQuery',
              menuname: 'Resource Apply',
              hasThird: 'N',
              url: 'goods/Apply',
              menus: null
            },
            {
              menuid: 2,
              icon: 'icon-cat-skuQuery',
              menuname: 'My Resource',
              hasThird: 'N',
              url: 'goods/Goods',
              menus: null
            }
          ]
        },
        {
          menuid: 33,
          icon: 'li-icon-dingdanguanli',
          menuname: 'Bill Center',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 34,
              icon: 'icon-provider-manage',
              menuname: 'Bill Management',
              hasThird: 'N',
              url: 'pay/Order',
              menus: null
            },
            {
              menuid: 159,
              icon: 'icon-provider-manage',
              menuname: 'Bill Analytics',
              hasThird: 'N',
              url: 'charts/statistics2',
              menus: null
            }
            // {
            //   menuid: 160,
            //   icon: 'icon-provider-manage',
            //   menuname: 'Bill Analytics2',
            //   hasThird: 'N',
            //   url: 'charts/statistics',
            //   menus: null
            // }
          ]
        },
        
        {
          menuid: 128,
          icon: 'li-icon-shangchengxitongtubiaozitihuayuanwenjian91',
          menuname: 'Cloud Lab',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 129,
              icon: 'icon-provider-manage',
              menuname: 'Cloud Materials',
              hasThird: 'N',
              url: 'machine/MachineConfig',
              menus: null
            },
            {
              menuid: 175,
              icon: 'icon-provider-manage',
              menuname: 'Best Practice',
              hasThird: 'N',
              url: 'pay/Config',
              menus: null
            }
          ]
        },
        {
          menuid: 151,
          icon: 'li-icon-shangchengxitongtubiaozitihuayuanwenjian91',
          menuname: 'DevOps',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 158,
              icon: 'icon-provider-manage',
              menuname: 'DevOps Apply',
              hasThird: 'N',
              url: 'goods/devops',
              menus: null
            }
          ]
        },
        {
          menuid: 71,
          icon: 'li-icon-xitongguanli',
          menuname: 'System Management',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 72,
              icon: 'icon-cus-manage',
              menuname: 'User Management',
              hasThird: 'N',
              url: 'system/user',
              menus: null
            },
            {
              menuid: 174,
              icon: 'icon-cms-manage',
              menuname: 'Menu Management',
              hasThird: 'N',
              url: 'system/Module',
              menus: null
            },
            {
              menuid: 73,
              icon: 'icon-news-manage',
              menuname: 'Role Management',
              hasThird: 'N',
              url: 'system/Role',
              menus: null
            },
            {
              menuid: 74,
              icon: 'icon-cs-manage',
              menuname: 'Company Management',
              hasThird: 'N',
              url: 'system/Dept',
              menus: null
            },
            {
              menuid: 75,
              icon: 'icon-promotion-manage',
              menuname: 'System Env',
              hasThird: 'N',
              url: 'system/Variable',
              menus: null
            },
            {
              menuid: 76,
              icon: 'icon-cms-manage',
              menuname: 'Authority management',
              hasThird: 'N',
              url: 'system/Permission',
              menus: null
            }
          ]
        }
      ],
      msg: 'success'
    }
          this.allmenu = res.data
    
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
    this.$root.Bus.$on('toggle', value => {
      this.collapsed = !value
    })
  },
  methods:{
    backhome(){
      this.$router.push('/')
    }
  }
  
}
</script>
<style>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 240px;
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
  height: 40px;
  line-height: 40px;
  color: #9d9d9d;
  font-size: 20px;
  text-align: left;
  margin-left: 30px;
  padding: 20px 0px;
}
.logoimg {
  height: 30px;
}
.cloudhub.el-button--text{
  color:#000;
  
}
el-menu-item is-active{
  color: #000;
}
</style>