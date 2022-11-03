<script setup lang="ts">
  import { reactive } from "vue";
  interface IProps {
    email?: string;
    password?: string;
  }

  const props = withDefaults(defineProps<IProps>(), {
    email: "student001@jedlik.eu",
    password: "student001",
  });

  interface IReactiveData {
    email: string;
    password: string;
  }

  const r = reactive<IReactiveData>({
    email: props.email,
    password: props.password,
  });
</script>

<template>
  <q-dialog>
    <q-card>
      <q-input v-model="r.email" />
    </q-card>
  </q-dialog>
</template>

<style lang="scss" scoped></style>
