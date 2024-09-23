<template>
  <RouterView></RouterView>
  <v-container fluid class="welcome-page">
    <v-row align="center" justify="center">
      <v-col cols="12" md="8" sm="8" xs="8">
        <v-card color="purple" class="text-center d-block">
          <v-card-title>
            <h2 class="white--text">Welcome to AHMES Messaging App!</h2>
          </v-card-title>
          <v-card-text>
            <p class="mb-4 white--text">
              Our centralized official Message notification system for <strong>AHMES</strong> Schools.
            </p>
            <v-btn color="white" @click="openLoginDialog">Login</v-btn>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>

    <!-- Include the LoginForm component -->
    <LoginForm ref="loginForm" />
  </v-container>
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
