<template>
  <v-text-field v-bind="props" v-model="value" :error-messages="errors" :loading="meta.pending" @blur="(e: FocusEvent) => handleBlur(e, true)" />
</template>

<script setup lang="ts">
import { useField } from 'vee-validate';
import type { VTextField } from 'vuetify/components';
import type { Except, Props } from './util';

type CleanedProps = Except<Props<typeof VTextField>, 'modelValue' | 'errorMessages' | 'variant'>;

interface ExtendedProps extends /* @vue-ignore */ CleanedProps {
  name: string;
  label: string;
  id: string;
}

const props = withDefaults(defineProps<ExtendedProps>(), {
  type: 'text'
});

const { value, handleBlur, errors, meta } = useField<any>(() => props.name, undefined);
</script>
