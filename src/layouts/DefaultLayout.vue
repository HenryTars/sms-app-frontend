<template>
  <v-app>
    <v-navigation-drawer
      expand-on-hover
      rail
      v-model="drawer"
    >
      <v-list>
        <v-list-item
          prepend-avatar="https://randomuser.me/api/portraits/women/85.jpg"
          subtitle="upendo_01@gmail.com"
          title="Upendo Baraka"
        ></v-list-item>
      </v-list>

      <v-divider></v-divider>

      <v-list density="compact" nav>
        <v-list-item prepend-icon="mdi-view-dashboard" to="dashboard" title="Dashboard" value="dashboard"></v-list-item>
        <v-list-item prepend-icon="mdi-message-bulleted" to="messages" title="Messages" value="messages"></v-list-item>
        <v-list-item prepend-icon="mdi-account-multiple" to="contacts" title="Contacts" value="shared"></v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar density="compact" elevation="2" app class="bg-purple">
      <v-btn icon @click="toggleDrawer">
        <v-icon>mdi-menu</v-icon>
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn icon @click="logout">
        <v-icon>mdi-logout</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container fluid>
        <slot>

        </slot>
      </v-container>
    </v-main>

    <v-footer app>
      <v-container>
        <span class="text-caption grey">&copy; Designed and developed by Henry Tarsian Kemibara</span>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: true,
      username: 'John Doe', // Replace with dynamic username if needed
    };
  },
  methods: {
    toggleDrawer() {
      this.drawer = !this.drawer;
    },
    logout() {
      // Add logout logic here
      console.log('Logging out...');
    },
  },
};
</script>

<style scoped>
.v-footer {
  height: 30px; /* Adjust footer height */
}
</style>
