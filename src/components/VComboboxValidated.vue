<template>
    <v-combobox 
    v-bind="props" 
    v-model="value" 
    :error-messages="errors" 
    clearable 
    multiple 
    chips 
    @blur="(e: FocusEvent) => handleBlur(e, true)">
        <template v-for="(_, slotName) in ($slots as Slots)" :key="slotName" #[slotName]="slotProps">
            <slot :name="slotName" v-bind="slotProps"></slot>
        </template>
    </v-combobox>
</template>
  
<script setup lang="ts">
import { useField } from 'vee-validate';
import type { VCombobox } from 'vuetify/components';
import type { Except, Props } from './util';
import type { ExtractPropTypes } from 'vue';

type CleanedProps = Except<Props<typeof VCombobox>, 'itemValue' | 'errorMessages' | 'variant'>;

interface ExtendedProps extends /* @vue-ignore */ CleanedProps {
    name: string;
    label: string;
    id: string;
    items?: readonly unknown[];
}

const props = defineProps<ExtendedProps>();

// slots
type Slots = ExtractPropTypes<VCombobox['$slots']>;

defineSlots<Slots>();

const { value, handleBlur, errors } = useField<unknown[]>(() => props.name);
</script>
  