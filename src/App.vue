<template>
    <div>
        <h1>Страница с постами</h1>
        <MyButton
        @click="showDialog"
        >Создать пользователя</MyButton>
        <myDialog v-model:show="dealogVisible">
            <PostForm
            @create="createPost"
            ></PostForm>
        </myDialog>
        <PostList 
        :posts="posts"
        @remove="removePost"
        v-if="!isPostLoading"
        ></PostList>
        <div v-else>Загрузка...</div>
    </div>
</template>

<script>
import PostForm from "@/components/postForm.vue";
import PostList from "@/components/postList.vue"; 
import axios from "axios";
import MyButton from "./components/UI/MyButton.vue";

export default {
    components: {
    PostForm,
    PostList,
    MyButton
}, 
    data() {
        return {
            posts: [],
            dealogVisible: false,
            isPostLoading: false
        }
    },
    methods: {
        createPost(post) {
            if(post.title !== '' && post.body !== '') {
                this.posts.push(post);
                this.dealogVisible = false
                
            } else {
                alert('введите значение');
            }
        },
        inputText(event) {
            this.title = event.target.value;
        },
        removePost(post) {
            // this.posts = this.posts.filter(p => p.id !== post.id);
            this.posts = this.posts.filter(el => el.id !== post.id);
        },
        showDialog() {
            this.dealogVisible = true;
        },
        async fetchPost() {
            try {
                this.isPostLoading = true;
                
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                    this.posts = response.data;
            } catch (e) {
                alert(e, 'errors')
            } 
            finally {
                this.isPostLoading = false;
            }
            
        }
    },
    mounted() {
        this.fetchPost();
    }
}
</script>

<style scoped lang="scss">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
</style>
