<template>
    <div>
      <label :for="inputId">{{ label }}</label>
      <input
        :id="inputId"
        type="text"
        :value="modelValue"
        required
        @input="$emit('update:modelValue', $event.target.value)"
      >
      <div class="error" v-if="error">{{ error }}</div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      modelValue: String,
      label: String,
      error: String,
      inputId: String,
    },
    emits: ['update:modelValue'],
  }
  </script>