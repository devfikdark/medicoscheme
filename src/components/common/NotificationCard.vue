<template>
  <v-alert outlined prominent text :color="notificationInfo.is_view === false ? 'green darken-2' : 'grey darken-1'">
    <v-row>
      <v-col cols="8">
        <div class="title font-weight-bold">{{ notificationInfo.header }}</div>
      </v-col>
      <v-col cols="4" class="d-flex justify-end">
        <div class="caption">
          {{ moment(notificationInfo.createdAt).fromNow() }}
        </div>
      </v-col>
    </v-row>
    <p class="mt-2">
      {{ notificationInfo.details }}
    </p>
  </v-alert>
</template>

<script>
import moment from "moment";

export default {
  props: ["notificationInfo"],

  data: () => ({
    moment,
  }),
};
</script>

<style lang="scss" scoped></style>
