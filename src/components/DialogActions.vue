<template>
  <v-divider />
  <v-card-actions class="pa-5">
    <v-spacer />
    <v-btn id="cancel-btn" color="primary" variant="text" data-cy="close" @click="emits('close')">
      Close
    </v-btn>
    <v-btn
      v-if="actionButton"
      id="create-btn"
      color="primary"
      type="submit"
      variant="elevated"
      :loading="actionButton.loading"
      :disabled="actionButton.disabled"
      data-cy="submit"
    >
      {{ actionButton.text }}
    </v-btn>
  </v-card-actions>
</template>

<script setup lang="ts">

defineProps<{
    closeText: 'close' | 'cancel';
    actionButton?: {
        text: string;
        loading?: boolean;
        disabled?: boolean;
    };
}>();

const emits = defineEmits(['close', 'submit']);
</script>