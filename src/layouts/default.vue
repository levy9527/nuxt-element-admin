<template>
  <el-container>
    <side-bar />
    <div class="main-container">
      <main-head />
      <el-main class="nuxt-main">
        <nuxt></nuxt>
      </el-main>
      <el-footer>
        <copyright></copyright>
      </el-footer>
    </div>
  </el-container>
</template>

<script>
import Copyright from '../components/copyright.vue'
import MainHead from '@/container/main-head/index.vue'
import {mapState} from 'vuex'
import auth from '@/mixins/auth'
import SideBar from '@/container/side-bar/index.vue'

export default {
  mixins: [auth],
  components: {
    Copyright,
    SideBar,
    MainHead
  },
  data() {
    return {
      collapse: false
    }
  },
  computed: {
    ...mapState(['menuList'])
  }
}
</script>

<style lang="less">
#__nuxt {
  .el-icon-sort {
    transform: rotate(-90deg);
  }

  // main
  .nuxt-main {
    margin: 10px 20px 0;
    padding: 10px;
    background: #fff;
  }

  // dropdown
  .el-dropdown-link {
    cursor: pointer;
    color: #409eff;
  }

  .el-icon-arrow-down {
    font-size: 12px;
  }

  .main-container {
    height: 100vh;
    overflow-y: scroll;
  }
}
</style>
