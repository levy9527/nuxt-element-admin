<template>
  <div class="layout-login">
    <div class="login-form">
      <h1 class="title">
        {{ $store.state.meta.appName }}
      </h1>
      <nuxt></nuxt>
    </div>
    <div class="buttom-wrapper font-s text-center ">
      <copyright></copyright>
    </div>
  </div>
</template>

<script>
import Copyright from '../components/copyright.vue'
export default {
  name: 'login',
  components: {
    Copyright
  },
  data() {
    return {}
  },
  methods: {}
}
</script>
<style lang="less">
@basic-font-family: PingFangSC-Regular;

.layout-login {
  position: absolute;
  padding: 8% 0 0;
  width: 100%;
  min-height: 100%;
  background-color: #f0f2f5;
  background-image: url(https://deepexi.oss-cn-shenzhen.aliyuncs.com/xpaas-console/bg_login.png);
  background-repeat: no-repeat;
  background-size: 100% 100%;

  .logo-login {
    width: 260px;
    vertical-align: middle;
  }

  .title {
    position: relative;
    height: 34px;
    line-height: 34px;
    margin: 0 auto 45px;
    text-align: center;
    font-size: 38px;
    font-family: 'Myriad Pro', 'Helvetica Neue', Arial, Helvetica, sans-serif;
    font-weight: 600;
    color: #5d81f9;
  }

  .login-form {
    width: 450px;
    margin: 0 auto 100px;
    padding: 50px 0 20px;
    background: #fff;
    box-shadow: 0 4px 10px 0 rgba(0, 0, 0, 0.1);
  }

  .buttom-wrapper {
    width: 100%;
    position: absolute;
    bottom: 19px;

    .buttom-link {
      height: 17px;
      line-height: 17px;
      font-family: @basic-font-family;
      margin-bottom: 11px;

      a {
        color: rgba(255, 255, 255, 1);
      }

      .service-item {
        margin: 0 24px;
        cursor: pointer;
      }
    }

    .copyright {
      height: 17px;
      line-height: 17px;
      font-size: 12px;
      font-family: @basic-font-family;
      color: #606266;
    }
  }

  .main {
    width: 300px;
    margin: auto;
  }

  .el-form {
    width: 100%;
    margin: auto;
  }

  .el-button {
    width: 300px;
    margin: auto;
    display: block;
    height: 40px;
    border-radius: 35px;
  }
}
</style>
