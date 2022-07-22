<template>
    <input
            class="posts__inputAddPost"
            :placeholder="placeholder"
            type="text"
            :value="modelValue"
            @input="updateInput"
    >
</template>

<script>
    export default {
        name: 'PostFormInput',
        props : {
            modelValue:String,
            placeholder:String
        },
        methods:{
            updateInput(event){
                this.$emit('update:modelValue', event.target.value)
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