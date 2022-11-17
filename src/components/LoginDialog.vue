<script setup lang="ts">
  import { useAppStore } from "src/store/appStore";
  import { useUsersStore } from "src/store/usersStore";
  import { reactive, computed } from "vue";
  interface IProps {
    email?: string;
    password?: string;
  }

  const props = withDefaults(defineProps<IProps>(), {
    email: "student001@jedlik.eu",
    password: "student001",
  });

  // const emit = defineEmits<{
  //   // eslint-disable-next-line no-unused-vars
  //   (e: "close-login-dialog"): void;
  // }>();

  interface IReactiveData {
    email: string;
    password: string;
  }

  const r = reactive<IReactiveData>({
    email: props.email,
    password: props.password,
  });

  const usersStore = useUsersStore();
  const appStore = useAppStore();

  const anyLoggedUser = computed(() => (usersStore.getLoggedUser ? true : false));

  function LoginLogout() {
    if (anyLoggedUser.value) {
      usersStore.logOut();
    } else {
      usersStore.loginUser({
        email: r.email,
        password: r.password,
      });
    }
  }
</script>

<template>
  <q-dialog
    v-model="appStore.showLoginDialog"
    full-width
    persistent
    transition-hide="rotate"
    transition-show="rotate"
  >
    <q-card class="q-pa-lg" style="width: 100%">
      <q-form>
        <q-card-section>
          <q-input v-model="r.email" :disable="anyLoggedUser" label="E_mail address" />
        </q-card-section>
        <q-card-section v-if="!anyLoggedUser">
          <q-input v-model="r.password" label="Password" type="password" />
        </q-card-section>
        <q-card-actions align="center">
          <q-btn
            class="q-mr-md"
            color="green"
            :label="anyLoggedUser ? 'Logout' : 'Login'"
            no-caps
            @click="LoginLogout()"
          />
          <q-btn
            color="red"
            label="Close dialog"
            no-caps
            @click="appStore.showLoginDialog = false"
          />
        </q-card-actions>
      </q-form>
    </q-card>
  </q-dialog>
</template>

<style lang="scss" scoped></style>
