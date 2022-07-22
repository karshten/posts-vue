<template>
    <div class="postItem__main-part">
        <img class="postItem__img"
             :src="post.img ? post.img : 'default-img.png'"
             @error="post.img = 'default-img.png' "
             alt="post.title">
        <div class="postItem__text">
            <h3>{{post.title}}</h3>
            <p>{{slicedDesc}}</p>
            <PostButton v-if="post.description.length > 50" @click="handleMoreDesc">
                {{showDescription ? 'hide': 'show more...'}}
            </PostButton>
        </div>
    </div>
    <PostButton @click="handelDeletePost">Delete</PostButton>
</template>

<script>

    export default {
        data() {
            return {
                showDescription: false,
                slicedDesc: this.post.description.slice(0, 50)
            }
        },
        props: {
            post:{
                type:Object,
                required:true,
                img:{
                    default:'default-img.png'
                }
            }
        },
        methods: {
            handleMoreDesc(){
                if (this.showDescription) {
                    this.slicedDesc = this.post.description.slice(0, 50)
                    this.showDescription = !this.showDescription
                } else {
                    this.slicedDesc = this.post.description
                    this.showDescription = !this.showDescription
                }
        },
            handelDeletePost(){
                this.$emit('removePost', this.post)
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