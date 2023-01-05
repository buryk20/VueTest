<template>
    <div>
        <PostForm
        @create="createPost"
        ></PostForm>
        <PostList 
        :posts="posts"
        @remove="removePost"
        ></PostList>
    </div>
</template>

<script>
import PostForm from "@/components/postForm.vue";
import PostList from "@/components/postList.vue"; 

export default {
    components: {
        PostForm,
        PostList
    }, 
    data() {
        return {
            posts: [
                {id: 1, title: 'JavaScrit', description: 'Описание поста'},
                {id: 2, title: 'JavaScrit2', description: 'Описание поста2'},
                {id: 3, title: 'JavaScrit,3', description: 'Описание поста,3'}
            ]
        }
    },
    methods: {
        createPost(post) {
            if(post.title !== '' && post.description !== '') {
                this.posts.push(post);
                
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
        }
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
