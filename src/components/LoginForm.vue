<template>
  <v-dialog v-model="dialog" max-width="400">
    <v-card padding="4px">
      <v-card-title class="text-center bg-grey bold">
        <v-icon large class="mr-2">mdi-key-chain-variant</v-icon> <!-- Larger key icon -->
        <h2 class="text-h6 strong">Login to your Account</h2> <!-- Updated title -->
      </v-card-title>
      <v-card-text>
        <v-form ref="form" v-model="valid">
          <v-text-field
            clearable
            prepend-icon="mdi-account"
            variant="outlined"
            v-model="username"
            label="Username"
            :rules="[rules.required]"
            required
          ></v-text-field>
          <v-text-field
            clearable
            prepend-icon="mdi-lock"
            variant="outlined"
            v-model="password"
            label="Password"
            :rules="[rules.required]"
            type="password"
            required
          ></v-text-field>
          <v-btn block variant="elevated" color="purple" @click="submit">Login</v-btn>
          <v-btn block color="red" class="mt-2" @click="closeDialog">Cancel</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      username: '',
      password: '',
      valid: false,
      rules: {
        required: value => !!value || 'This field is required',
      },
    };
  },
  methods: {
    openDialog() {
      this.dialog = true;
    },
    closeDialog() {
      this.dialog = false;
      this.username = '';
      this.password = '';
    },
    submit() {
      if (this.$refs.form.validate()) {
        // Handle login logic here
        console.log('Username:', this.username);
        console.log('Password:', this.password);

        // Redirect to the dashboard
        this.$router.push('/dashboard'); // Adjust the route as necessary

        this.closeDialog();
      }
    },
  },
};
</script>

<style scoped>
/* Add any specific styles for your login form here */
</style>
