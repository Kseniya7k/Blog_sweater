<template>
    <div>
        <ul>
            <Post
            v-for="post of posts"
            v-bind:post = "post"
            v-bind:currentUser = "currentUser"
            v-bind:key = "post.date"
            v-on:remove-text="removeText"
            v-on:transform-post="transformPost"
            />
        </ul>
    </div>
</template>

<script>
import Post from '@/components/Post'
export default {
    props: ['posts', 'currentUser'],
    methods: {
        removeText(date) {
            this.$emit('remove-text', date)
        },
        transformPost(date, value) {
            this.$emit('transform-post', date, value)
        }
    },
    components: {
        Post
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>