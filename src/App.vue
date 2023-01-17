<template>
    <div>
        <h1 class="app__title">Страница с постами</h1>
        <MyInput
            v-model="searchQuery"
            class="app__search-input"
            placeholder=" Поиск...."
        ></MyInput>
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
        :posts="sortedAndSearchedPosts"
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
import MyInput from "./components/UI/MyInput.vue";

export default {
    components: {
    PostForm,
    PostList,
    MyButton,
    MyInput
},
    data() {
        return {
            posts: [],
            dealogVisible: false,
            isPostLoading: false,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPage: 0,
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
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    
                params: {
                    _page: this.page,
                    _limit: this.limit
                }
                });
                this.posts = response.data;
                this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit);
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
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
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

    &__search-input {
        margin-bottom: 16px;
    }
}
</style>
