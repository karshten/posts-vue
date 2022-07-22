<template>
    <main class="posts">
        <div class="posts__menu">
            <PostButton @click="showModal">
                Create post
            </PostButton>
            <PostFilter
                    v-model="filteredBy"
                    :options="forFilterOptions"
            />
        </div>
        <ModalDialog v-model:show="modalOpen">
            <PostForm
                    :posts="posts"
                    @createPost="createPost"
            />
        </ModalDialog>
        <div class="posts-content__findPost">
            <PostFormInput
                    class="findPost__input"
                    v-model="searchQuery"
                    :placeholder="'search post...'"/>
        </div>
        <PostList v-if="isPostGot"
                  :posts="searchPosts"
                  @removePost="removePost"
        />
        <h2 v-else>Loading Posts...</h2>
    </main>
</template>

<script>
    import PostList from "./components/PostList";
    import PostForm from './components/PostForm'
    import ModalDialog from "./components/UI/ModalDialog";
    import PostButton from "./components/UI/PostButton";
    import PostFilter from "./components/UI/PostFilter";

    export default {
        components: {PostFilter, PostButton, ModalDialog, PostForm, PostList},
        data() {
            return {
                posts: [],
                isPostGot: false,
                modalOpen: false,
                filteredBy: '',
                searchQuery: '',
                forFilterOptions: [
                    {value: 'title', name: "sort by title"},
                    {value: 'description', name: "sort by description"},
                ]
            }
        },
        mounted() {
            fetch(`http://localhost:3000/posts`)
                .then(res => res.json())
                .then(data => {
                    setTimeout(() => {
                        this.posts = data
                        this.isPostGot = true
                    }, 1000)
                })
        },
        methods: {
            createPost(newPost) {
                this.posts.push(newPost)
                this.modalOpen = false
            },
            removePost(targetPost) {
                this.posts = this.posts.filter(post => {
                    return post.id !== targetPost.id
                })
            },
            showModal() {
                this.modalOpen = true
            }
        },
        computed: {
            filteredPosts() {
                return [...this.posts].sort((post1, post2) => {
                    return post1[this.filteredBy]?.localeCompare(post2[this.filteredBy])
                })
            },
            searchPosts(){
                return this.filteredPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
            }
        },
        // watch:{
        //     filteredBy(newValue){
        //         this.posts.sort((post1, post2)=>{
        //             return post1[newValue]?.localeCompare(post2[newValue])
        //         })
        //     }
        // }
    }
</script>
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        font: 16px sans-serif;
        margin: 0;
        padding: 0;
    }

    .posts {
        padding: 20px;
        max-width: 1200px;
        margin: 0 auto;
    }

    .posts__menu {
        display: flex;
        justify-content: space-between;
    }
</style>