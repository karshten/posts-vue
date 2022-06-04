<template>
    <form>
        <input
                v-model="post.title"
                class="posts__inputAddPost"
                type="text"
                placeholder="Названте поста">
        <input
                v-model="post.description"
                class="posts__inputAddPost"
                type="text"
                placeholder="Описание">
        <input
                v-bind:value="this.img"
                @input="post.img = $event.target.value"
                class="posts__inputAddPost"
                type="text"
                placeholder="Фото(ссылка)">
        <button
                @click="createPost(post)"
                type="button"
                class="posts__btnAddPost postItem__btn">Добавить
        </button>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                post: {
                    title: '',
                    description: '',
                    img: ''
                }
            }
        },
        props: {
            posts: {
                type: Array,
                required: true,
            }
        },
        methods: {
            createPost(newPost) {
                this.posts.push(newPost)
                this.title = ''
                this.description = ''
                this.img = ''
            }
        }
    }
</script>

<style scoped>

    .posts__inputAddPost {
        width: 60%;
        padding: 5px;
        margin-bottom: 15px;
        border: 1px solid #3e8969;
    }
</style>