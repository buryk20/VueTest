<template>
    <div v-if="posts.length > 0">
        <h3>Список пользователей</h3>
        <PostItem 
        v-for="post in posts"
        :post="post" 
        :key="post.id"
        @remove="$emit('remove', post)"
        ></PostItem>
    </div>
    <div v-else>
        <h2>список постов пуст</h2>
    </div>
    
</template>

<script>
import PostItem from './postItem.vue';

export default {
    props: {
        posts: {
            type: Array,
            required: true
        }
    },
    components: { PostItem }
}
    
</script>

<style lang="scss" scoped>

</style>