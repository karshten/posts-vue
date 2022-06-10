<template>
    <SectionTitle>
        {{sectionTitle}}
        <template v-slot:desc>
            <p class="posts__title__desc">{{mainDesc}}</p>
        </template>
    </SectionTitle>
    <ul class="posts__posts-content">
        <template v-for="(post,i) in posts">
            <li v-if="i < showCount" :key="post.id" class="content__postItem">
                <post-item
                        :img="post.img"
                        :title="post.title"
                        :description="post.description"
                />
            </li>
        </template>
        <PostButton
                v-if="showCount < posts.length" class="postBtn"
                @click="showMore"
        >Смотреть больше
        </PostButton>
    </ul>
</template>

<script>
    import PostButton from "./UI/PostButton";
    import PostItem from './PostItem'
    import SectionTitle from "./UI/SectionTitle";

    export default {
        components: {PostItem, PostButton, SectionTitle},
        props: {
            posts: {
                type: Array,
                required: true
            }
        },
        data() {
            return {
                showCount: 3,
                sectionTitle:'Posts',
                mainDesc:`Posts about best JS libraries/frameworks`
            }
        },
        methods: {
            showMore() {
                this.showCount += 3
            }
        }
    }
</script>

<style>
    .posts__posts-content {
        width: 100%;
        list-style: none;
    }
    .content__postItem {
        padding: 15px;
        margin-bottom: 20px;
        display: flex;
        justify-content: space-between;
        border: 2px solid #3e8969;
        align-items: center;
    }
</style>