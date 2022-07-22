<template>
    <button class="postBtn">
        <slot></slot>
    </button>
</template>

<script>
    export default {
        name:'PostButton'
    }
</script>

<style>
    .postBtn {
        display: block;
        background: #3e8969;
        padding: 8px 16px;
        cursor: pointer;
        border: none;
        color: #fff;
        border-radius: 3px;
    }
</style>