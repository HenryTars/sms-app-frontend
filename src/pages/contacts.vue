<template>
  <DefaultLayout>
    <div class="contacts-container">
      <h2>Contacts</h2>

      <v-row align="center" justify="space-between" class="mb-4">
        <v-col cols="auto">
          <v-btn color="primary" @click="showAddContactDialog">
            Add New Contact
          </v-btn>
        </v-col>
        <v-col cols="4">
          <v-text-field
            v-model="search"
            label="Search Contacts"
            append-inner-icon="mdi-magnify"
            density="compact"
            variant="outlined"
            rounded="xl"
            hide-details
          ></v-text-field>
        </v-col>
      </v-row>

      <v-card>
        <v-card-title>Registered Contacts</v-card-title>
        <v-card-text>
          <v-list>
            <v-list-item-group>
              <v-list-item
                v-for="(contact, index) in paginatedContacts"
                :key="index"
                class="contact-item"
              >
                <div class="d-flex justify-space-between align-center w-100">
                  <v-list-item-content>
                    <v-list-item-title>{{ contact.name }}</v-list-item-title>
                    <v-list-item-subtitle>{{ contact.email }}</v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-action>
                    <v-btn variant="" icon @click="editContact(contact)">
                      <v-icon size="sm" color="success">mdi-pencil</v-icon>
                    </v-btn>
                    <v-btn variant="" size="sm" icon @click="deleteContact(index)">
                      <v-icon color="error">mdi-delete</v-icon>
                    </v-btn>
                  </v-list-item-action>
                  <v-divider></v-divider>
                </div>
              </v-list-item>
            </v-list-item-group>
          </v-list>

          <v-pagination
            v-model="currentPage"
            :length="totalPages"
            class="mt-4"
            rounded="circle"
          ></v-pagination>
        </v-card-text>
      </v-card>

      <v-dialog v-model="addContactDialog" max-width="600px">
        <v-card>
          <v-card-title>Add New Contact</v-card-title>
          <v-card-text>
            <v-form ref="form">
              <v-text-field
                v-model="newContact.name"
                label="Name"
                required
              ></v-text-field>
              <v-text-field
                v-model="newContact.email"
                label="Email"
                required
              ></v-text-field>
              <v-text-field
                v-model="newContact.phone"
                label="Phone"
                required
              ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" @click="addContact">Add</v-btn>
            <v-btn @click="addContactDialog = false">Cancel</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
  </DefaultLayout>
</template>

<script>
import DefaultLayout from '@/layouts/DefaultLayout.vue';

export default {
  components: {
    DefaultLayout,
  },
  data() {
    return {
      contacts: [
        { name: 'John Doe', email: 'john@example.com', phone: '555-0123' },
        { name: 'Jane Smith', email: 'jane@example.com', phone: '555-0456' },
        { name: 'Alice Johnson', email: 'alice@example.com', phone: '555-0789' },
        // Add more contacts as needed
      ],
      search: '',
      currentPage: 1,
      itemsPerPage: 5,
      addContactDialog: false,
      newContact: {
        name: '',
        email: '',
        phone: '',
      },
    };
  },
  computed: {
    filteredContacts() {
      const searchLower = this.search.toLowerCase();
      return this.contacts.filter(contact =>
        contact.name.toLowerCase().includes(searchLower) ||
        contact.email.toLowerCase().includes(searchLower)
      );
    },
    paginatedContacts() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      return this.filteredContacts.slice(start, start + this.itemsPerPage);
    },
    totalPages() {
      return Math.ceil(this.filteredContacts.length / this.itemsPerPage);
    },
  },
  methods: {
    showAddContactDialog() {
      this.addContactDialog = true;
    },
    addContact() {
      if (this.newContact.name && this.newContact.email && this.newContact.phone) {
        this.contacts.push({ ...this.newContact });
        this.newContact = { name: '', email: '', phone: '' }; // Reset form
        this.addContactDialog = false;
      } else {
        alert('Please fill in all fields.');
      }
    },
    editContact(contact) {
      // Implement editing functionality
      alert(`Editing contact: ${contact.name}`);
    },
    deleteContact(index) {
      if (confirm('Are you sure you want to delete this contact?')) {
        this.contacts.splice(index, 1);
      }
    },
  },
};
</script>

<style scoped>
.contacts-container {
  padding: 20px;
}
.contact-item {
  display: flex;
  justify-content: space-between;
}
</style>
