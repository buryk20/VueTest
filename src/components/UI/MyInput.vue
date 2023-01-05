<template>
    <input 
    @input="updateInput"
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
            // this.$emit('update:myValue', event.target.value);
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