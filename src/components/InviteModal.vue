<template>
  <v-dialog v-model="visible" max-width="45vw" scrollable>
    <template #activator="{ props }">
      <v-tooltip location="top" :text="'Invite'">
        <template #activator="{ props: tooltip }">
          <v-btn color="primary" v-bind="{ ...props, ...tooltip }" icon="mdi-account-plus" />
        </template>
      </v-tooltip>
    </template>
    <v-card>
      <form>
        <v-card-text>
          <v-row>
            <v-col class="py-0">
              <v-text-field-validated id="user-email" name="userEmail" label="Email" />
              <v-text-field-validated id="user-name" name="userName" label="Name" />
            </v-col>
          </v-row>
        </v-card-text>

        <DialogActions close-text="cancel" @close="cancel()" />
      </form>
    </v-card>
  </v-dialog>
</template>

<script lang="ts" setup>
import { ref, watch, nextTick } from 'vue';
import VTextFieldValidated from './VTextFieldValidated.vue';
import { object, string, type InferType } from 'yup';
import { useForm } from 'vee-validate';
import DialogActions from './DialogActions.vue';

const visible = ref(false);

const cancel = () => {
  visible.value = false;
};

const schema = object({
  userName:  string().required().label("Name"),
  userEmail: string().required().email().label("Email"),
});

type UserForm = InferType<typeof schema>;

const defaultForm: UserForm = {
  userName: '',
  userEmail: ''
};

const { resetForm } = useForm({
  validationSchema: schema,
  initialValues: defaultForm
});

watch(
  () => visible.value,
  () => {
    nextTick(() =>  resetForm())   
  }
);
</script>
