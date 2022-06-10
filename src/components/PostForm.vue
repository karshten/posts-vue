<template>
    <SectionTitle>
        {{title}}
        <template #desc="">
            <p class="posts__title__desc">{{mainDesc}}</p>
        </template>
    </SectionTitle>
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
                v-model="post.img"
                class="posts__inputAddPost"
                type="text"
                placeholder="Фото(ссылка)">
        <PostButton
                @click="createPost"
                type="button">
                Создать
        </PostButton>
    </form>
</template>

<script>
    import PostButton from "./UI/PostButton";
    import SectionTitle from "./UI/SectionTitle";

    export default {
        components: {PostButton,SectionTitle},
        data() {
            return {
                title: 'Add post',
                mainDesc:`If you know fascinating feature about JS, you can share it`,
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
            createPost() {
                this.post.id = this.posts.length + 1
                this.$emit('createPost', this.post)
                this.post = {
                    title: '',
                    description: '',
                    img: ''
                }
            }
        }
    }
</script>

<style>

    .posts__inputAddPost {
        width: 60%;
        padding: 5px;
        margin-bottom: 15px;
        border: 1px solid #3e8969;
    }
</style>