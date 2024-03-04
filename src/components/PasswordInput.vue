<template>
    <div>
        <label for="password">Password:</label>
        <input id="password" type="password" :value="modelValue" required
            @input="$emit('update:modelValue', $event.target.value)" />
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