<template>
  <v-container>
    <div v-if="isLoading">
      <v-overlay :value="isLoading">
        <v-progress-circular indeterminate size="64"></v-progress-circular>
      </v-overlay>
    </div>
    <div v-else>
      <div class="display-1 text-center font-weight-bold mb-4">Notification List</div>
      <div class="d-flex justify-end align-center mb-6" v-if="unSeenNotifications.length > 0">
        <v-btn plain color="secondary" class="text-capitalize" @click="markToSeen">Mark All As Read</v-btn>
      </div>
      <v-row>
        <v-col cols="12" v-for="notification in notifications" :key="notification.id">
          <notification-card :notificationInfo="notification" />
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script>
import { mapGetters, mapState } from "vuex";
import NotificationCard from "../../components/common/NotificationCard.vue";

export default {
  components: { NotificationCard },

  created() {
    this.$store.dispatch("common/getAllNotifications");
  },

  computed: {
    ...mapState(["isLoading"]),
    ...mapState("common", ["notifications"]),
    ...mapGetters("common", ["unSeenNotifications"]),
  },

  methods: {
    markToSeen() {
      this.$store.dispatch("common/seenNotifications");
    },
  },
};
</script>

<style lang="scss" scoped></style>
