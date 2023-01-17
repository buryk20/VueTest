<template>
    <div v-if="posts.length > 0">
        <h3>Список пользователей</h3>
        <transition-group name="user-list">
            <PostItem 
            v-for="post in posts"
            :post="post" 
            :key="post.id"
            @remove="$emit('remove', post)"
            ></PostItem>
        </transition-group>
        
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

    .user-list-item {
    display: inline-block;
    margin-right: 10px;
    }

    .user-list-enter-active,
    .user-list-leave-active {
        transition: all 0.3s ease;
    }
    .user-list-enter-from,
    .user-list-leave-to {
        opacity: 0;
        transform: translateX(30px);
    }

    .user-list-move {
        transition: transform 0.8s ease;
      }

</style>