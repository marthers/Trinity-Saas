<style lang="less">
  @import './login.less';
</style>

<template>
  <div class="login">
    <div class = "login-left">
        <div class = "login-logo-name">
            <div class = "login-logo" src="./../../assets/images/ShunXiangLogo.png" alt="舜翔众邦"></div>
            <div class = "login-name">
                舜翔科技有限公司
            </div>
        </div>
        <p class = "login-slogen">
            自助设备运营管理平台
        </p>
    </div>
    <div class="login-con">
        <div class = "tabs-con">
            <div :class = "[!selectPassword ? '' : 'login-select' , 'password-login']" @click = "passwordSelected">密码登录</div>
            <div class = "tabs-line"></div>
            <div :class = "[!selectPassword ? 'login-select' : '' , 'verify-login']"  @click = "verifySelected">验证码登录</div>
        </div>
        <Input v-model="userName" :placeholder="userNamePlaceholder" number autofocus maxlength="11" class = "login-input"/>
        <Input v-model="password" placeholder="请输入密码" autofocus  class = "login-input" v-if = "selectPassword" />
        <Input v-model="verifyCode" placeholder="请输入验证码" autofocus  class = "verify-input" v-if = "!selectPassword"  search enter-button="获取验证码"/>
        <div class = "two-button">
            <div class = "remember-login" v-if = "selectPassword">
              <div v-show= "notRemember" class = "not-remember-login" @click="notRemember = !notRemember"></div>
              <div v-show = "!notRemember" class = "remember-login" @click="notRemember = !notRemember"></div>
              <p>
                记住密码
              </p>
            </div>
            <div class = "forgotten-password">
              忘记密码
            </div>
        </div>
        <div class = "login-button main-button">登录</div>
        <div class = "login-button  main-button">注册</div>
    </div>
  </div>
</template>

<script>
import LoginForm from '_c/login-form'
import { mapActions } from 'vuex'
export default {
  components: {
    LoginForm
  },
  data () {
    return {
      selectPassword: true,
      userName: '',
      password: '',
      verifyCode: '',
      userNamePlaceholder: '请输入用户名',
      notRemember: true
    }
  },
  methods: {
    ...mapActions([
      'handleLogin',
      'getUserInfo'
    ]),
    handleSubmit ({ userName, password }) {
      this.handleLogin({ userName, password }).then(res => {
        this.getUserInfo().then(res => {
          this.$router.push({
            name: this.$config.homeName
          })
        })
      })
    },
    passwordSelected () {
      this.selectPassword = true
      this.userNamePlaceholder = '请输入用户名'
    },
    verifySelected () {
      this.selectPassword = false
      this.userNamePlaceholder = '请输入手机号'
    }
  }
}
</script>

<style>

</style>
