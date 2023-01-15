<template>
    <div>
        <h1 class="app__title">Страница с постами</h1>
        <div class="app__btns">
            <MyButton
            @click="showDialog"
            >
                Создать пользователя
            </MyButton>
            <mySelect
                :options="sortOptions"
                v-model="selectedSort"
            ></mySelect>
        </div>

        <myDialog v-model:show="dealogVisible">
            <PostForm
            @create="createPost"
            ></PostForm>
        </myDialog>
        <PostList
        :posts="sortedPosts"
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
            isPostLoading: false,
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По описанию'},
                {value: 'id', name: 'id'}
            ]
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
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => {
                if(typeof post1[this.selectedSort] === "number") {
                    return post2[this.selectedSort] - post1[this.selectedSort];
                } else {
                    return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]);
                } 
            });
        }
    },
    // watch: {
    //     selectedSort(newValue) {
    //         this.posts.sort((post1, post2) => {
    //             if(typeof post1[newValue] === "number") {
    //                 return post2[newValue] - post1[newValue];
    //             } else {
    //                 return post1[newValue]?.localeCompare(post2[newValue]);
    //             }
                    
    //         });
            
    //     }
    // }
}
</script>

<style scoped lang="scss">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    &__btns {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    &__title {
        margin-bottom: 16px;
    }
}
</style>
