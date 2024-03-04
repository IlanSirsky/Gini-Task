<template>
    <label for="phone">Phone number: </label>
    <div class="phoneNum">
        <select v-model="selectedPrefix" required @change="$emit('update:prefix', selectedPrefix)">
            <option value="050">050</option>
            <option value="052">052</option>
            <option value="054">054</option>
        </select>
        <p>-</p>
        <input id="phone" type="text" :value="number" required @input="$emit('update:number', $event.target.value)">
    </div>
    <div class="error" v-if="error">{{ error }}</div>
</template>

<script>
export default {
    props: {
        prefix: String,
        number: String,
        error: String,
    },
    data() {
        return {
            selectedPrefix: this.prefix,
        };
    },
}
</script>