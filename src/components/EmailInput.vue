<template>
    <div>
        <label for="email">Email:</label>
        <input id="email" type="email" :value="modelValue" required @input="$emit('update:modelValue', $event.target.value)" />
        <div class="error" v-if="error">{{ error }}</div>
    </div>
</template>

<script>
export default {
    props: {
        modelValue: String,
        error: String,
    },
    emits: ['update:modelValue'],
}
</script>