<template>
  <input :value="modelValue" :type="type" @input="updateModel($event.target.value)" />
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

defineProps({
  modelValue: String,
  type: {
    type: String,
    default: 'text'
  }
});

const emit = defineEmits(['update:modelValue']);

function updateModel(value) {
  emit('update:modelValue', value);
}
</script>