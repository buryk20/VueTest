<template>
    <input
    @input="updateInput"
    :value="modelValue"
    class="input"
    >
</template>

<script>
export default {
    name: 'MyInput',
    props: {
        modelValue: [String, Number]
        // myValue: [String]
    },
    methods: {
        updateInput(event) {
            this.$emit('update:modelValue', event.target.value);
            // this.modelValue = '';
        }
    }
}
</script>

<style lang="scss" scoped>
.input {
    width: 100%;
    margin-top: 20px;
    border: 1px solid red;
}
</style>