<template>
  <div id="app">
    <div class="container">
      <div class="module">
        <form class="layui-form layui-form-pane" action="">
          <div class="layui-form-item">
            <label class="layui-form-label">用户名</label>
            <div class="layui-input-inline">
              <input type="text" name="username" v-model="username"  placeholder="请输入用户名" autocomplete="off" class="layui-input">
            </div>
            <div class="layui-form-mid layui-word-aux">辅助文字</div>
          </div>
          <div class="layui-form-item">
            <label class="layui-form-label">密码</label>
            <div class="layui-input-inline">
              <input type="password" name="password" v-model="password" placeholder="请输入密码" autocomplete="off" class="layui-input">
            </div>
            <div class="layui-form-mid layui-word-aux">辅助文字</div>
          </div>
          <div class="layui-form-item">
            <label class="layui-form-label">验证码</label>
            <div class="layui-input-inline">
              <input type="password" name="password" v-model="code" placeholder="请输入验证码" autocomplete="off" class="layui-input">
            </div>
            <div class="layui-form-mid Captcha" @click="getCaptcha()" v-html="captcha">辅助文字</div>
          </div>
          <div class="layui-form-item">
            <div class="layui-input-inline">
              <button type="button" class="layui-btn">点击登录</button>
              <a href="" class="link" >忘记密码？</a>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  props: {},
  data () {
    return {
      captcha: null,
      username: null,
      password: null,
      code: null
    }
  },
  mounted () {
    this.getCaptcha()
  },
  methods: {
    getCaptcha () {
      axios.get('http://localhost:3000/getCaptcha').then((res) => {
        if (res.status === 200) {
          const obj = res.data
          this.captcha = obj.data
        } else {
          return false
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  #app{
    width: 100%;
    height: 100vh;
    background-color: #f2f2f2;
    .container{
      margin: 0 auto;
      width: 1200px;
      .module{
        padding: 30px 40px;
        background-color: #ffffff;
        .Captcha{
          position: relative;
          top: -10px;
        }
        .link{
          margin-left: 12px;
          &:hover{
            color: #009688;
          }
        }
      }
    }
  }
</style>
