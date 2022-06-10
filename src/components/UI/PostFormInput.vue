<template>
    <input
            v-model="post.postValue"
            class="posts__inputAddPost"
            :placeholder="placeholder"
            type="text"
    >
</template>

<script>
    export default {
        name: 'PostFormInput',
        props:{
            post:{
                type:Object
            },
            postValue: String,
            placeholder:String
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