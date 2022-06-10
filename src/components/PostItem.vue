<template>
    <div class="postItem__main-part">
        <img class="postItem__img"
             :src="img ? img : 'default-img.png'"
             @error="img = 'default-img.png' "
             alt="post.title">
        <div class="postItem__text">
            <h3>{{title}}</h3>
            <p>{{showDescription}}</p>
            <PostButton @click="handleMoreDesc" href="">подробнее</PostButton>
        </div>
    </div>
    <PostButton>Удалить</PostButton>
</template>

<script>
    import PostButton from "./UI/PostButton";

    export default {
        components: {PostButton},
        data() {
            return {
                showDescription: this.description.slice(0, 50)+'...'
            }
        },
        props: {
            img: {
                type:String,
                default: 'default-img.png'
            },
            title: String,
            description: String
        },
        methods:{
            handleMoreDesc (){
                this.showDescription = this.description
            }
        }
    }
</script>

<style>

    .postItem__img {
        max-width: 120px;
        max-height: 150px;
        margin-right: 15px;
    }

    .postItem__main-part {
        max-width: 60%;
        display: flex;
        align-items: center;
    }

    .postItem__main-part p {
        margin: 6px 0;
    }

    .postItem__main-part a {
        color: #3e8969;
        text-decoration: none;
    }
</style>