<template>
    <el-menu mode="vertical" :default-active="$route.path"  background-color="#304156" text-color="#bfcbd9" active-text-color="#409EFF">
       <!-- :collapse="isCollapse"> -->
      <template>
        <el-menu-item index="" class="submenu-title-noDropdown">
          <h2>devEops 3.0</h2>
        </el-menu-item>
      </template>
      <sidebar-item :routes="routers" :types="'deveops'"></sidebar-item>
      <!--:collapse="isCollapse"-->
    </el-menu>
</template>

<script>
  import { mapGetters } from 'vuex'
  import SidebarItem from '@/components/SidebarItem/index'
  export default {
    name:'Sidebar',
    components: {
      SidebarItem 
    },
    computed:{
      ...mapGetters([
        'routers'
      ])
    }
  }
</script>
<style rel="stylesheet/scss" lang="scss">

</style>
