<template>
  <div class="header-wrap">
    <el-row class="head-container" type="flex" justify="end" align="middle">
      <el-col>
        <el-row
          class="right-container"
          type="flex"
          justify="end"
          align="middle"
        >
          <div class="icon-button">
            <i class="el-icon-share"></i>
          </div>
          <div class="icon-button">
            <i class="el-icon-edit"></i>
          </div>
          <div class="icon-button">
            <i class="el-icon-question"></i>
          </div>
          <div class="icon-button">
            <el-badge :value="12">
              <i class="el-icon-message"></i>
            </el-badge>
          </div>
          <div class="head-right">
            <div class="head-active">
              <img :src="userImg" class="userName-Img" alt="userName-Img" />
            </div>
            <!-- 用户名称 -->
            <div class="userName-text">{{ $store.state.user.nickname }}</div>
            <el-dropdown placement="bottom-end" @command="exitBtn">
              <span class="el-dropdown-link">
                <i class="el-icon-arrow-down el-icon--right set-Iconcolor"></i>
              </span>
              <el-dropdown-menu slot="dropdown" class="user-drop-menu">
                <el-dropdown-item
                  v-for="(item, index) of dropdownList"
                  :key="index"
                  :command="item.command"
                  >{{ item.title }}</el-dropdown-item
                >
              </el-dropdown-menu>
            </el-dropdown>
          </div>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import {mapMutations} from 'vuex'

export default {
  name: 'MainHead',
  data() {
    return {
      dropdownList: [
        {
          title: '退出',
          command: 'exit'
        }
      ]
    }
  },
  computed: {
    userImg() {
      return (
        this.$store.state.user.avatar ||
        'https://deepexi.oss-cn-shenzhen.aliyuncs.com/xpaas-console/user-portrait.png'
      )
    },
    ...mapMutations(['logout'])
  },
  methods: {
    exitBtn(key, keyPath) {
      if (key == 'exit') {
        this.$store.commit('logout')
      }
    }
  }
}
</script>

<style lang="less">
.header-wrap {
  height: 60px;
  padding: 0 24px;
  box-shadow: 0 1px 4px rgba(0, 21, 41, 0.08);
  background: #fff;

  .head-container {
    height: 100%;
  }

  .right-container {
    .icon-button {
      padding: 10px 15px;

      > i {
        font-size: 18px;
      }
    }
  }

  .head-right {
    margin-right: 20px;
    display: flex;
    align-items: center;

    div {
      display: inline-block;
    }

    .head-active {
      .userName-Img {
        width: 30px;
        height: 30px;
        border-radius: 50%;
        margin: 0 15px;
      }
    }

    .userName-text {
      text-align: center;
      overflow: hidden;
      margin-right: 10px;
    }

    .head-search {
      .set-search {
        margin-right: 5px;
      }

      .head-autocomplete {
        .el-icon-search {
          cursor: pointer;
          font-size: 18px;
        }
      }

      .el-dropdown-link {
        font-size: 18px;
        color: #a2a2b1 !important;
      }
    }

    .head-message {
      margin: 0 30px 0 20px;

      .item {
        .set-IconSize {
          height: 100%;
          max-width: 100%;
        }
      }
    }
  }
}
</style>
