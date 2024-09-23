<template>
  <h1>Hellooooo</h1>
</template>

<script>
import LoginForm from '@/components/LoginForm.vue';

export default {
  components: {
    LoginForm,
  },
  methods: {
    openLoginDialog() {
      this.$refs.loginForm.openDialog();
    },
  },
};
</script>

<style scoped>
.welcome-page {
  background-color: #f5f5f5;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.v-card {
  border-radius: 6px; /* Optional: Add rounded corners */
}

.white--text {
  color: white; /* Ensures text is white for better readability */
}
</style>
