<template>
    <div class="post">
        <div>
            <div>
                <strong>Название:</strong>
                {{post.title}}
            </div>
            <div>
                <strong>Описание:</strong>
                {{post.body}}
            </div>
        </div>
        <div class="post__btns">
            <MyButton
            @click="$emit('remove', post)"
            >Удалить</MyButton>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        post: {
            type: Object,
            required: true
        }
    }
}
</script>

<style lang="scss" scoped>
.post {
    margin-top: 16px;
    padding: 16px;
    border: 2px solid red;
} 
</style>