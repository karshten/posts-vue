<template>
    <SectionTitle>
        {{sectionTitle}}
        <template #desc="">
            <p class="posts__title__desc">{{mainDesc}}</p>
        </template>
    </SectionTitle>
    <form>
        <PostFormInput
                :placeholder="'Название поста'"
                :post="post"
                :post-value="post.title"
        />
        <PostFormInput
                :placeholder="'Описание поста'"
                :post="post"
                :post-value="post.description"
        />
        <PostFormInput
                :placeholder="'Картинка поста'"
                :post="post"
                :post-value="post.img"
        />
        <PostButton
                @click="createPost"
                type="button">
                Создать
        </PostButton>
    </form>
</template>

<script>
    import SectionTitle from "./UI/SectionTitle";
    import PostFormInput from "./UI/PostFormInput";
    import PostButton from "./UI/PostButton";

    export default {
        components: {PostFormInput, PostButton,SectionTitle},
        data() {
            return {
                sectionTitle: 'Add post',
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

</style>