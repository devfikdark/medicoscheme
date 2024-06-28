<template>
  <div>
    <v-navigation-drawer v-model="drawer" app>
      <sidebar-options />
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title class="font-weight-medium">Medico Scheme</v-toolbar-title>

      <v-spacer></v-spacer>
      <router-link :to="role === 'patient' ? '/patient/notification' : role === 'lab' ? '/lab/notification' : '/doctor/notification'">
        <v-badge overlap color="green" class="mr-6" :value="unSeenNotifications.length" :content="unSeenNotifications.length" v-if="role !== 'admin'">
          <v-icon>
            mdi-bell
          </v-icon>
        </v-badge>
      </router-link>
      <v-btn outlined class="text-capitalize" color="red" @click="handleLogout"> Logout <v-icon right>mdi-logout-variant</v-icon> </v-btn>
    </v-app-bar>
  </div>
</template>

<script>
import { mapGetters, mapState } from "vuex";
import SidebarOptions from "./SidebarOptions.vue";
export default {
  components: { SidebarOptions },
  data: () => ({
    drawer: null,
  }),
  created() {
    this.$store.dispatch("common/getAllNotifications");
  },
  computed: {
    ...mapGetters("common", ["unSeenNotifications"]),
    ...mapState("auth", ["role"]),
  },
  methods: {
    handleLogout() {
      this.isLoading = true;

      this.$store.dispatch("auth/logout");
    },

    routeToNotificationPage() {
      if (this.role === "patient") {
        return "/patient/notification";
      } else if (this.role === "doctor") {
        return "/doctor/notification";
      } else if (this.role === "lab") {
        return "/lab/notification";
      }
    },
  },
};
</script>
