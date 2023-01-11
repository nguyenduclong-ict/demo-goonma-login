<template>
  <div>
    <el-button @click="logout">Logout</el-button>
  </div>
</template>

<script>
export default {
  auth: true,
  name: "IndexPage",

  methods: {
    async logout() {
      await this.$auth.logout({
        data: {
          refresh_token: this.$auth.strategy.refreshToken.get(),
        },
      });
      window.location.reload();
    },
  },
};
</script>
