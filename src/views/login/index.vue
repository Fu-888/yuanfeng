<template>
  <div class="main">
    <div class="login-container">
      <div class="left">
        <div class="title">
          <img src="../../imgs/title.ef005a7a.png" alt="" />
        </div>
        <el-form
          :model="loginForm"
          :rules="loginRules"
          label-width="100px"
          ref="loginFormRef"
        >
          <div class="users">
            <div class="divImg"><img src="../../imgs/下载.png" alt="" /></div>
            <!-- <el-form-item prop="pass">
              <el-input type="password" autocomplete="off"></el-input>
            </el-form-item> -->
            <div class="divInput">
              <el-form-item prop="username">
                <el-input
                  v-model="loginForm.username"
                  placeholder="请输入内容"
                ></el-input
              ></el-form-item>
            </div>
          </div>
          <div class="pwd">
            <div class="divimgs">
              <img src="../../imgs/下载2.png" alt="" />
            </div>
            <div class="divpwd">
              <el-form-item prop="password">
                <el-input
                  type="password"
                  v-model="loginForm.password"
                  placeholder="请输入密码"
                  show-password
                ></el-input>
              </el-form-item>
            </div>
          </div>
        </el-form>
        <div class="checkBox">
          <el-checkbox v-model="checked">记住密码</el-checkbox>
        </div>
        <el-button @click="login">立即登录</el-button>
      </div>
      <div class="right"></div>
    </div>
  </div>
</template>

<script>
import { validUsername } from '@/utils/validate'
export default {
  name: 'Login',
  data() {
    const validateUsername = (rule, value, callback) => {
      if (!validUsername(value)) {
        callback(new Error('Please enter the correct user name'))
      } else {
        callback()
      }
    }
    const validatePassword = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('The password can not be less than 6 digits'))
      } else {
        callback()
      }
    }
    return {
      checked: false,
      loginForm: {
        username: 'admin',
        password: '111111'
      },
      loginRules: {
        username: [
          { required: true, trigger: 'blur', validator: validateUsername }
        ],
        password: [
          { required: true, trigger: 'blur', validator: validatePassword }
        ]
      },
      loading: false,
      passwordType: 'password',
      redirect: undefined
    }
  },
  watch: {
    $route: {
      handler(route) {
        this.redirect = route.query && route.query.redirect
      },
      immediate: true
    }
  },
  methods: {
    async login() {
      try {
        await this.$refs.loginFormRef.validate()
        this.$router.push('/')
        this.loading = false
      } catch (e) {
        console.log('e', e)
        this.loading = false
      }
    }
  }
}
</script>

<style lang="scss">
/* 修复input 背景不协调 和光标变色 */
/* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

$bg: #283443;
$light_gray: #fff;
$cursor: #fff;

@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
  .login-container .el-input input {
    // color: $cursor;
  }
}
</style>
<style lang="scss" scoped>
.main {
  background-color: #fdfafa;
  .login-container {
    width: 958px;
    height: 516px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    box-shadow: 0 0 20px rgb(93 93 93 / 33%);
    background-color: #fff;
    border-radius: 40px;

    .left {
      .el-form-item {
        margin-bottom: 22px;
        // background-color: #f8f5f5;
      }
      float: left;
      width: 398px;
      height: 516px;
      background: #fff;
      border-radius: 34px 0 0 34px;
      margin: 0 auto;
      .title {
        margin-left: 124px;
        margin-top: 72px;
        img {
          width: 150px;
          height: 64px;
        }
        .user {
          margin-left: 59px;
          width: 280px;
          height: 50px;
        }
        .el-input__inner {
          width: 230px;
          height: 50px;
          line-height: 50px;
          background-color: #f8f5f5;
          border-bottom-left-radius: 0;
          border-top-left-radius: 0;
        }
      }
      .checkBox {
        margin-top: 22px;
        margin-left: 63px;
      }
      .el-button {
        margin-top: 15px;
        margin-left: 59px;
      }
      .users {
        display: flex;
        margin-top: 50px;
        margin-left: 59px;
        width: 280px;
        height: 50px;
        .divImg {
          width: 50px;
          height: 50px;
          background: #eae7e7;
          border-radius: 8px 0 0 8px;
          img {
            width: 25px;
            height: 24px;
            margin: 12px 13px;
          }
        }
        .divInput {
          display: flex;
          width: 230px;
          height: 50px;
          background-color: #f8f5f5;
        }
      }
      .pwd {
        display: flex;
        margin-top: 50px;
        margin-left: 59px;
        width: 280px;
        height: 50px;
        .divimgs {
          width: 50px;
          height: 50px;
          background: #eae7e7;
          border-radius: 8px 0 0 8px;
          img {
            width: 25px;
            height: 24px;
            margin: 12px 13px;
          }
        }
        .divpwd {
          display: flex;
          width: 230px;
          height: 50px;
          background-color: #f8f5f5;
        }
      }
    }
  }
  .right {
    float: right;
    background-image: url(../../imgs/contentBg.1321d126.png);
    background-position: 50%;
    background-repeat: no-repeat;
    background-size: cover;
    width: 560px;
    height: 516px;
  }
  .el-button {
    width: 280px;
    height: 50px;
    background: #ffb200;
    border-radius: 8px;
    box-shadow: 0 2px 9px 1px rgb(255 178 0 / 47%);
    font-size: 16px;
    font-weight: 600;
    text-align: center;
    color: #332929;
    line-height: 22px;
  }
  // .el-input__inner {
  //   width: 230px;
  //   height: 50px;
  //   background-color: #f8f5f5;
  //   border-bottom-left-radius: 0;
  //   border-top-left-radius: 0;
  // }
  // .el-input {
  //   display: inline-block;
  //   width: 100%;
  // }
  // .el-form-item__content {
  //   margin: unset;
  //   width: 50px;
  // }
  ::v-deep .el-input__inner {
    border-radius: 0 4px 4px 0;
    height: 50px;
    line-height: 50px;
    width: 230px;
    margin-left: -100px !important;
    background: #f8f5f5;
  }
}
</style>
