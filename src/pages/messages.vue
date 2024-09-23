<template>
  <DefaultLayout>
    <v-card class="mt-8 mx-auto overflow-visible">
      <v-sheet
        class="v-sheet--offset mx-auto py-3"
        align="center"
        color="cyan"
        elevation="1"
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
            label="Search messages..."
            variant="outlined"
            hide-details
            rounded="xl"
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
  </DefaultLayout>
</template>

<script>
import DefaultLayout from '@/layouts/DefaultLayout.vue';

export default {
  components: {
    DefaultLayout
  },
  data() {
    return {
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
    }
  }
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

