<template>
    <div>
        <form @submit.prevent>
            <h4>Создания поста</h4>
            <MyInput  
            v-model="post.title"
            ref
            type="text" 
            placeholder="Название"></MyInput>
            <MyInput 
            v-model="post.body"
            type="text" 
            placeholder="Описание"></MyInput>
            <MyButton
            @click="createPost"
            >Добавить</MyButton>
        </form>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    data() {
        return {
            post: {
                title: "",
                body: ""
            }
        };
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit("create", this.post);
            // console.log(this.post.title);
            // console.log(modelValue);
            // this.post = {
            //     title: "",
            //     body: ""
            // };
            
            // this.$emit("create", this.post);
        }
    }
}

</script>

<style lang="scss" scoped>

</style>