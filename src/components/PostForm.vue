<template>
    <SectionTitle>
        {{sectionTitle}}
        <template #desc="">
            <p class="posts__title__desc">{{mainDesc}}</p>
        </template>
    </SectionTitle>
    <form>
        <PostFormInput
                v-model="post.title"
                :placeholder="'post name...'"
        />
<!--        v-model.trim-->
<!--        v-model.number-->
<!--        v model |modification|-->
        <PostFormInput
                v-model="post.description"
                :placeholder="'post description...'"
        />
        <PostFormInput
                v-model="post.img"
                :placeholder="'post image...'"
        />
        <PostButton
                @click="createPost"
                type="button">
            create
        </PostButton>
    </form>
</template>

<script>

    export default {
        data() {
            return {
                sectionTitle: 'Add post',
                mainDesc: `If you know fascinating feature about JS, you can share it`,
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
        },
        // watch:{
        //     post(newValue){
        //         console.log(newValue)
        //     }
        // }
        // watch:{
        //    post:{
        //        handler(newValue){
        //            console.log(newValue)
        //        },
        //        deep:true
        //    }
        // }
    }
</script>

<style>

</style>