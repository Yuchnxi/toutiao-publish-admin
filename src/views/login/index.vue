<template>
  <div class="login-container">
    <!--
      el-form 表单组件
      每个表单项都必须使用 el-form-item 组件包裹
     -->

    <div class="login-form-wrap">
      <div class="login-head">
        <div class="logo"></div>
      </div>
      <!--
        配置 Form 表单验证：
        1、必须给 el-from 组件绑定 model 为表单数据对象
        2、给需要验证的表单项 el-form-item 绑定 prop 属性
           注意：prop 属性需要指定表单对象中的数据名称
        3、通过 el-from 组件的 rules 属性配置验证规则
          具体的验证规则可以参考：https://github.com/yiminghe/async-validator
          如果内置的验证规则不满足，也可以自定义验证规则
        手动触发表单验证：
        1、给 el-form 设置 ref 起个名字（随便起名，不要重复即可）
        2、通过 ref 获取 el-form 组件，调用组件的 validate 进行验证
       -->
      <el-form
        class="login-form"
        ref="login-form"
        :model="user"
      >
        <el-form-item prop="mobile">
          <el-input
            v-model="user.mobile"
            placeholder="请输入手机号"
          ></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <el-input
            v-model="user.code"
            placeholder="请输入验证码"
          ></el-input>
        </el-form-item>
        <el-form-item prop="agree">
          <el-checkbox v-model="user.agree">我已阅读并同意用户协议和隐私条款</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button
            class="login-btn"
            type="primary"
            @click="onLogin"
          >登录</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
import request from '@/utils/request'
export default {
  name: "loginIndex",
  data() {
    return {
      user: {
        mobile: "", // 手机号
        code: "", // 验证码
      },
      checked: false // 是否同意协议的选中状态
    }
  },
  components: {},
  created () {},
  mounted () {},
  methods: {
    onLogin () {
      const user = this.user

      request({
        method: 'POST',
        url: ' /mp/v1_0/authorizations',
        data: user
      }).then(res => {
        console.log(res)
      })
    }
  }
}
</script>
<style lang='less' scoped>
.login-container {
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: url("./login_bg.jpg") no-repeat;
  background-size: cover;
  .login-form-wrap {
    min-width: 300px;
    padding: 30px 50px 10px;
    background-color: #fff;
    .login-head {
      display: flex;
      justify-content: center;
      .logo {
        width: 200px;
        height: 57px;
        background: url("./logo_index.png") no-repeat;
        background-size: contain;
      }
    }
    .login-form {
      .login-btn {
        width: 100%;
      }
    }
  }
}
</style>
