<template>
    <button  class="btn">
       <slot></slot>
    </button>
</template>

<script>
export default {
    name: 'MyButton'
}
</script>

<style lang="scss" scoped>
.btn {
    padding: 10px 16px;
    border: 1px solid blue;
    cursor: pointer;
}
</style>