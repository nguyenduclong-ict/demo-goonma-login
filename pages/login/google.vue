<template>
  <div></div>
</template>

<script>
const waitFor = (ms) => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, ms);
  });
};

export default {
  auth: "guest",
  async fetch() {
    const loading = this.$loading({ text: "Đang đăng nhập..." });
    try {
      // Chờ ít nhất 2s để tránh spam login
      const wait = waitFor(2000);
      const { state, code } = this.$route.query;
      const res = await this.$axios.$post("/user/logingoogle", {
        state,
        code,
      });
      this.$auth.setUserToken(res.data.token, res.data.refresh_token);
      await wait;
      location.href = "/";
      loading.close();
    } catch (error) {
      console.error();
      location.href = "/";
    }
    loading.close();
  },
};
</script>

<style lang="scss" scoped></style>
