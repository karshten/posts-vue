<template>
    <button class="postBtn">
        <slot></slot>
    </button>
</template>

<script>
    export default {

    }
</script>

<style scoped>
    .postBtn {
        display: block;
        background: #3e8969;
        padding: 4px 7px;
        cursor: pointer;
        border: none;
        color: #fff;
        border-radius: 3px;
    }
</style>