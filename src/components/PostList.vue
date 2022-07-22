<template>
    <SectionTitle>
        {{sectionTitle}}
        <template v-slot:desc>
            <p class="posts__title__desc">{{mainDesc}}</p>
        </template>
    </SectionTitle>
    <ul v-if="posts.length" class="posts__posts-content">
        <transition-group name="post-list">
            <template v-for="(post,i) in posts" :key="post.id">
                <li v-if="i < showCount" class="content__postItem">
                    <post-item
                            @removePost="$emit('removePost', post)"
                            :post="post"
                    />
                </li>
            </template>
        </transition-group>
        <PostButton
                v-if="showCount < posts.length" class="postBtn"
                @click="showMore"
        >Show more posts
        </PostButton>
    </ul>
    <h2 v-else>No posts yet</h2>
</template>

<script>
    // import PostButton from "./UI/PostButton";
    // import SectionTitle from "./UI/SectionTitle";
    import PostItem from './PostItem'
    import PostFormInput from "./UI/PostFormInput";
    import PostButton from "./UI/PostButton";

    export default {
        components: {PostButton, PostFormInput, PostItem},
        props: {
            posts: {
                type: Array,
                required: true
            }
        },
        data() {
            return {
                showCount: 3,
                sectionTitle: 'Posts',
                mainDesc: `Posts about best JS libraries/frameworks`
            }
        },
        methods: {
            showMore() {
                this.showCount += 3
            }
        },
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

    .posts-content__findPost {
        margin: 20px 0;
    }

    .findPost__input {
        max-width: 40%;
        padding: 7px 5px;
    }ё

    .findPost__btn {
        display: inline-block;
        border-radius: 0 3px 3px 0;
    }

    .post-list-enter-active,
    .post-list-leave-active {
        transition: all .3s ease;
    }

    .post-list-enter-from,
    .post-list-leave-to {
        opacity: .0;
        transform: translateX(100px);
    }

    .post-list-move {
        transition: transform .3s ease;
    }
</style>