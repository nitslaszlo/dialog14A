<script setup lang="ts">
  import { computed } from "vue";
  import { useUsersStore } from "../store/usersStore";
  import { useAppStore } from "../store/appStore";
  import LoginDialog from "../components/LoginDialog.vue";

  const usersStore = useUsersStore();
  const appStore = useAppStore();

  // interface IReactiveData {
  //   showDialog: boolean;
  // }

  // const r = reactive<IReactiveData>({
  //   showDialog: false,
  // });

  const anyLoggedUser = computed(() => (usersStore.getLoggedUser ? true : false));
</script>

<template>
  <q-page>
    <div class="row window-height flex-center justify-evenly">
      <q-btn
        class="shadow-10"
        color="info"
        :label="anyLoggedUser ? 'Show logout dialog' : 'Show login dialog'"
        no-caps
        @click="appStore.showLoginDialog = true"
      />
      <q-btn
        class="shadow-10"
        color="blue"
        :label="anyLoggedUser ? 'Logout from Google' : 'Login/Register with Google'"
        no-caps
      />
      <!-- LoginDialog saját komponens helye -->
      <LoginDialog />
    </div>
  </q-page>
</template>

<style lang="scss" scoped></style>
