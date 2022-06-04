<template>
    <div v-for="(post,i) in posts">
        <li v-if="i < showCount" :key="post.id" class="content__postItem">
            <div class="postItem__main-part">
                <img class="postItem__img" :src="post.img" alt="post.title">
                <div class="postItem__text">
                    <h3>{{post.title}}</h3>
                    <p>{{post.description}}</p>
                    <a href="">подробнее</a>
                </div>
            </div>
            <button class="postItem__btn">Нравиться</button>
        </li>
    </div>
    <button v-if="showCount < posts.length" class="postItem__btn" @click="showMore">Смотреть больше..</button>
</template>

<script>
    export default {
        data() {
            return {
                showCount: 3,
            }
        },
        props: {
            posts: {
                type: Array,
                required: true,
            }
        },
        methods: {
            showMore() {
                this.showCount += 3
            }
        }
    }
</script>

<style scoped>
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

    .postItem__img {
        max-width: 150px;
        margin-right: 15px;
    }

    .postItem__main-part {
        max-width: 40%;
        display: flex;
        align-items: center;
    }
</style>