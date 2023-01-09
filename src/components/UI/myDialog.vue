<template>
    <div class="dialog" v-if="show" @click="hideDialog">
        <div @click.stop class="dialog__content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: 'myDialog',
    props: {
        show: {
            type: Boolean,
            default: false
        },
        a: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideDialog() {
            this.$emit('update:show', false);
            this.$emit('update:a', false);
        }
    },   
}
</script>

<style lang="scss" scoped>

.dialog {
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    display: flex;

    &__content {
        padding: 24px;
        margin: auto;
        background-color: #ffffff;
    }
}
</style>