<template>
  <div class="login">
    <LoginHeader>
      <el-form
        :model="ruleForm"
        label-position="left"
        label-width="0px"
        slot="container"
        :rules="rules"
        ref="ruleForm"
      >
        <div class="title">
          <h3>账号密码登录</h3>
        </div>
        <!-- username -->
        <el-form-item prop="username">
          <el-input
            type="text"
            v-model="ruleForm.username"
            auto-complete="off"
            placeholder="账号"
          >
            <i slot="prefix" class="fa fa-user"></i>
          </el-input>
        </el-form-item>
        <!-- password -->
        <el-form-item prop="pwd">
          <el-input
            type="password"
            v-model="ruleForm.pwd"
            auto-complete="off"
            placeholder="密码"
          >
            <i slot="prefix" class="fa fa-lock"></i>
          </el-input>
        </el-form-item>

        <!-- 登录button -->
        <el-form-item>
          <el-button
            :loading="isLogin"
            type="primary"
            @click.native.prevent="handleSubmit"
            style="width: 100%"
            >登录</el-button
          >
        </el-form-item>

        <!-- 七天登录 和 忘记密码 -->
        <el-form-item>
          <el-checkbox
            v-model="ruleForm.autoLogin"
            :checked="ruleForm.autoLogin"
          >
            七天自动登录
          </el-checkbox>
          <el-button
            @click="$router.push('/password')"
            type="text"
            class="forget"
            >忘记密码？</el-button
          >
        </el-form-item>
      </el-form>
    </LoginHeader>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Provide } from "vue-property-decorator";
import { State, Getter, Mutation, Action } from "vuex-class";
import LoginHeader from "./LoginHeader.vue";

@Component({
  components: { LoginHeader }
})
export default class Login extends Vue {
  // 存储用户信息
  @Action("setUser") setUser: any;

  private ruleForm: {
    username: String;
    pwd: String;
    autoLogin: boolean;
  } = {
    username: "",
    pwd: "",
    autoLogin: true // 自动登录
  };
  private isLogin: boolean = false;
  private rules = {
    username: [{ required: true, message: "请输入账号", trigger: "blur" }],
    pwd: [{ required: true, message: "请输入密码", trigger: "blur" }]
  };
<<<<<<< HEAD

=======
  created(){
    this.open2()
  }
>>>>>>> dcbef54... feat(product_list/import_list)
  handleSubmit(): void {
    (this.$refs["ruleForm"] as any).validate((valid: boolean) => {
      if (valid) {
        this.isLogin = true;
        (this as any).$axios
          .post("/api/users/login", this.ruleForm)
          .then((res: any) => {
            this.isLogin = false;
            console.log(res);
            // 存储token
            localStorage.setItem("tsToken", res.data.token);
            // 存储到vuex中
            this.setUser(res.data.token);

            // 登录成功跳转
            (this as any).$router.push("/");
          })
          .catch((err: any) => {
            console.log("没有请求成功");
            console.log(err);
            this.isLogin = false;
          });
      }
    });
  }
<<<<<<< HEAD
=======
  // 提示消息
  open2() {
    (this as any).$notify({
      title: '警告',
      message: '初始账号是：admin ;密码是：123456',
      type: 'warning',
       duration: 0
    });
  }
>>>>>>> dcbef54... feat(product_list/import_list)
}
</script>

<style lang="scss" scoped>
.title {
  margin: 0px auto 40px auto;
  text-align: center;
  color: #505458;
}
i {
  font-size: 14px;
  margin-left: 8px;
}
.forget {
  float: right;
}
</style>
