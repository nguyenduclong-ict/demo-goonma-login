<template>
  <div class="login-page">
    <el-form :rules="rules">
      <el-form-item label="Username">
        <el-input v-model="form.email"></el-input>
      </el-form-item>
      <el-form-item label="Password">
        <el-input v-model="form.password"></el-input>
      </el-form-item>

      <el-button @click="login">Login</el-button>
      <el-button @click="loginWithGoogle">Login With Google</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    const {
      data: { url },
    } = await $axios.$get("/user/getgoogleloginurl", {
      params: {
        redirect_uri: "http://localhost:3000/login/google",
      },
    });

    return {
      googleLoginUrl: url,
    };
  },
  data() {
    return {
      rules: {},
      form: {
        email: "level3.test@gmail.com",
        password: "a12345678X",
      },
    };
  },
  methods: {
    async login() {
      const res = await this.$auth.loginWith("local", {
        data: this.form,
      });
      console.log(res);
      window.location.reload();
    },
    loginWithGoogle() {
      window.location.href = this.googleLoginUrl;
    },
  },
};
</script>

<style lang="css">
.login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 90vh;
}
</style>
