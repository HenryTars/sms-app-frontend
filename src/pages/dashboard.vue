<template>
  <DefaultLayout>
    <VCol>
      <!-- Breadcumbs -->
      <v-breadcrumbs
        color="secondary"
        :items="items"
      >
        <template v-slot:divider>
          <v-icon color="secondary">mdi-slash-forward</v-icon>
        </template>
      </v-breadcrumbs>

      <VRow>
        <VCol cols="12" md="4">
          <v-card
            class="mt-8 mx-auto overflow-visible"
            max-width="400"
          >
            <v-sheet
              class="v-sheet--offset mx-auto py-3"
              align="center"
              color="primary"
              elevation="12"
              max-width="calc(100% - 32px)"
              rounded="lg"
            >
              <VText class="text-h6 font-weight-light">
                <VIcon size="30">mdi-account-multiple</VIcon>
                Contacts
              </VText>
            </v-sheet>

            <v-card-text class="pt-0">
              <div class="text-h6 font-weight-light mb-2">
                Registered Contacts: <span class="text-h5 text-grey font-weight-bold">0</span>
              </div>
              <div class="subheading font-weight-light text-grey">
                No new registrations this month
              </div>
              <v-divider class="my-2"></v-divider>

              <v-icon class="me-2" size="large">mdi-account-plus</v-icon>
              <span
                class="text-caption font-weight-light"
                @click="dialog = true"
                style="cursor: pointer; color: #1976D2;"
              >
                Click here to register new contact
              </span>
            </v-card-text>
          </v-card>
        </VCol>

        <!-- Register New Contact Dialog -->
        <v-dialog v-model="dialog" max-width="600px">
          <v-card>
            <v-card-title class="bg-purple py-6" align="center">Register New Contact</v-card-title>
            <v-card-text>
              <v-form ref="form">
                <v-row>
                  <v-col cols="12" md="6">
                    <v-text-field
                      label="Name"
                      v-model="newContact.name"
                      variant="underlined"
                      prepend-inner-icon="mdi-account"
                    ></v-text-field>
                  </v-col>

                  <v-col cols="12" md="6">
                    <v-select
                      variant="underlined"
                      label="Relationship"
                      v-model="newContact.relationship"
                      :items="relationships"
                      prepend-inner-icon="mdi-account-group"
                    ></v-select>
                  </v-col>
                </v-row>

                <v-text-field
                  variant="underlined"
                  label="Email"
                  v-model="newContact.email"
                  prepend-inner-icon="mdi-email"
                ></v-text-field>

                <v-text-field
                  variant="underlined"
                  label="Phone"
                  v-model="newContact.phone"
                  prepend-inner-icon="mdi-phone"
                ></v-text-field>

                <v-btn class="mb-2" block flat color="success" @click="registerContact">Register</v-btn>
                <v-btn block variant="outlined" @click="dialog = false">Cancel</v-btn>
              </v-form>
            </v-card-text>

          </v-card>
        </v-dialog>

        <VCol cols="12" md="8">
          <v-card class="mt-8 mx-auto overflow-visible">
            <v-sheet
              class="v-sheet--offset mx-auto py-3"
              align="center"
              color="success"
              elevation="12"
              max-width="calc(100% - 32px)"
              rounded="lg"
            >
              <VText class="text-h6 font-weight-light">
                <VIcon size="30">mdi-message-text</VIcon>
                Messages
              </VText>
            </v-sheet>

            <v-card-text class="pt-0">
              <v-row align="center" justify="space-between">
                <v-col
                  cols="auto"
                  class="d-flex align-center"
                >
                <v-icon class="me-2" size="large">mdi-message-plus</v-icon>
                  <span
                    class="text-caption font-weight-light"
                    @click="messageDialog = true"
                    style="cursor: pointer; color: #1976D2;"
                  >
                    Click here to compose new message
                  </span>
                </v-col>

                <v-col
                  cols="4"
                >
                <v-text-field
                  :loading="loading"
                  append-inner-icon="mdi-magnify"
                  density="compact"
                  label="Search..."
                  variant="outlined"
                  rounded="xl"
                  hide-details
                  single-line
                  @click:append-inner="onClick"
                ></v-text-field>
                </v-col>
              </v-row>
              <!-- <div class="subheading font-weight-light text-grey">
                No new messages
              </div> -->

              <v-list
                :items="messageItems"
                lines="three"
                item-props
              >
                <template v-slot:subtitle="{ subtitle }">
                  <div v-html="subtitle"></div>
                </template>
            </v-list>
            <v-pagination
              v-model="page"
              :length="4"
              rounded="circle"
            ></v-pagination>
            </v-card-text>
          </v-card>
        </VCol>
      </VRow>

      <!-- Compose New Message Dialog -->
      <v-dialog v-model="messageDialog" max-width="600px">
        <v-card>
          <v-card-title>Compose New Message</v-card-title>
          <v-card-text>
            <v-form ref="form">
              <v-text-field label="Recipient" v-model="newMessage.recipient"></v-text-field>
              <v-textarea label="Message" v-model="newMessage.content"></v-textarea>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" @click="sendMessage">Send</v-btn>
            <v-btn text @click="messageDialog = false">Cancel</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </VCol>
  </DefaultLayout>
</template>

<script>
import DefaultLayout from '@/layouts/DefaultLayout.vue';
import { VRow } from 'vuetify/components';

export default {
  components: {
    DefaultLayout,
  },
  data() {
    return {
      dialog: false, // For registering contacts
      messageDialog: false, // For composing messages
      items: [
        { title: 'Dashboard', disabled: false, href: 'dashboard' },
      ],
      messageItems: [
        { type: 'divider', inset: true },
        {
          prependAvatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg',
          title: 'Summer BBQ',
          subtitle: `<span class="text-primary">to Alex, Scott, Jennifer</span> &mdash; Wish I could come, but I'm out of town this weekend.`,
        },
        { type: 'divider', inset: true },
        {
          prependAvatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg',
          title: 'Summer BBQ',
          subtitle: `<span class="text-primary">to Alex, Scott, Jennifer</span> &mdash; Wish I could come, but I'm out of town this weekend.`,
        },
        { type: 'divider', inset: true },
      ],
      relationships: ['Father', 'Mother', 'Guardian'],
      newContact: {
        name: '',
        email: '',
        phone: '',
      },
      newMessage: { // Initialize newMessage
        recipient: '',
        content: '',
      },
    };
  },
  methods: {
    registerContact() {
      if (this.newContact.name && this.newContact.email && this.newContact.phone) {
        alert(`Contact registered: ${this.newContact.name}`);
        this.dialog = false;
        this.newContact = { name: '', email: '', phone: '' }; // Reset form
      } else {
        alert('Please fill in all fields.');
      }
    },
    sendMessage() {
      if (this.newMessage.recipient && this.newMessage.content) {
        alert(`Message sent to: ${this.newMessage.recipient}`);
        this.messageDialog = false;
        this.newMessage = { recipient: '', content: '' }; // Reset form
      } else {
        alert('Please fill in all fields.');
      }
    },
  },
};
</script>

<style scoped>
.v-card {
  margin-bottom: 20px;
}
</style>

<style>
.v-sheet--offset {
  top: -24px;
  position: relative;
}
</style>
