<template>
  <div :class="{hideSidebar: collapse}" class="sidebar-container">
    <el-menu
      :collapse="collapse"
      :default-active="$route.path"
      :collapse-transition="false"
      router
      class="aside-menu"
      :background-color="variables.menuBg"
      :text-color="variables.menuText"
    >
      <div class="logo">
        <nuxt-link to="/">
          <img class="logo-img" :src="$store.state.meta.logo" alt="logo" />
          <h1 class="logo-text">{{ $store.state.meta.appName }}</h1>
        </nuxt-link>
      </div>
      <el-scrollbar wrap-class="scrollbar-wrapper">
        <menu-item :menuList="menuList" @select="selectItem"></menu-item>
      </el-scrollbar>

      <div class="fix-btn-wrap">
        <div class="collapse-btn" @click="toggleCollapse">
          <img
            class="btn-icon"
            src="https://deepexi.oss-cn-shenzhen.aliyuncs.com/deepexi-services/%E5%B7%A6%E4%BE%A7%E8%8F%9C%E5%8D%95/expand.svg"
            alt=""
          />
        </div>
      </div>
    </el-menu>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import MenuItem from '../../components/menu-item.vue'
import IconFont from '../../components/icon-font.vue'
import variables from '../../assets/variables.less'

export default {
  name: 'Sidebar',
  data() {
    return {
      variables,
      appName: '应用标题'
    }
  },
  components: {
    MenuItem,
    IconFont
  },
  computed: {
    ...mapState(['menuList', 'collapse'])
  },
  methods: {
    selectItem(m) {
      this.$store.commit('update', {mainHeadTitle: m.name, ifShow: true})
    },
    toggleCollapse() {
      this.$store.commit('update', {collapse: !this.$store.state.collapse})
    }
  }
}
</script>

<style lang="less">
@import '../../assets/variables.less';

@title-bg: rgba(242, 244, 249, 1);
@menu-height: 50px;
@primary-color: #1890ff;

.sidebar-container {
  transition: width 0.28s;
  width: @sideBarMaxWidth !important;
  height: 100vh;
  overflow: hidden;
  box-shadow: 1px 0 6px rgba(0, 21, 41, 0.35);

  //reset element-ui css
  .horizontal-collapse-transition {
    transition:
      0s width ease-in-out,
 0s padding-left ease-in-out,
      0s padding-right ease-in-out;
  }

  .logo {
    position: relative;
    height: 60px;
    line-height: 60px;
    padding-left: 10px;
    background: @menuBg;
    overflow: hidden;

    .logo-img {
      /* width: 32px; */

      /* height: 32px; */
      vertical-align: middle;
    }

    .logo-text {
      color: #fff;
      display: inline-block;
      vertical-align: middle;
      font-size: 20px;
      margin: 0 0 0 5px;
      font-weight: 400;
      opacity: 1;
    }
  }

  .scrollbar-wrapper {
    height: calc(100vh - 110px);
    overflow-x: hidden !important;
    margin-bottom: 0 !important;

    .el-scrollbar__view {
      height: 100%;
    }
  }

  .el-scrollbar__bar.is-vertical {
    right: 0;
  }

  .is-horizontal {
    display: none;
  }

  .el-menu {
    border: none;
    height: 100%;
    width: 100% !important;

    .item-title {
      position: relative;

      &::before {
        content: '';
        display: inline-block;
        position: absolute;
        top: 50%;
        left: -12px;
        transform: translateY(-50%);
        bottom: 0;
        width: 5px;
        height: 5px;
        background: rgba(171, 172, 176, 1);
        border-radius: 1px;
      }
    }

    .el-menu-item {
      &.is-active {
        .item-title {
          &::before {
            width: 5px;
            height: 16px;
            background-color: @primary-color;
            border-radius: 15px;
          }
        }
      }
    }

    [class*='icon'] {
      font-size: 14px;
      margin-right: 5px;
    }
  }

  .fix-btn-wrap {
    height: 50px;

    .collapse-btn {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 50px;
      width: 100%;
      background: #343744;
      cursor: pointer;
    }

    .btn-icon {
      transform: rotate(180deg);
      font-size: 16px;
      width: 16px;
    }
  }

  // 折叠
  &.hideSidebar {
    width: @sideBarMinWidth !important;

    .logo {
      padding-left: 13px;
    }

    .scrollbar-wrapper {
      height: calc(100vh - 60px - 50px);
    }

    .el-submenu__title {
      text-align: center;
    }

    // 有子菜单
    .sub-menu-title,
    .el-submenu__icon-arrow {
      display: none;
    }

    [class*='icon'] {
      font-size: 16px;
      margin: 0;
    }

    .fix-btn-wrap {
      .btn-icon {
        transform: rotate(0deg);
      }
    }
  }

  // when menu collapsed
  .menu--vertical {
    // the scroll bar appears when the subMenu is too long
    > .menu--popup {
      max-height: 100vh;
      overflow-y: auto;

      &::-webkit-scrollbar {
        width: 6px;
      }

      &::-webkit-scrollbar-thumb {
        border-radius: 20px;
      }
    }
  }
}
</style>
