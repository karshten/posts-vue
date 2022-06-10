<template>
    <div>
        <h2 class="posts__title">
            <slot></slot>
        </h2>
        <slot name="desc"></slot>
    </div>
</template>

<script>
    export default {

    }
</script>

<style>
    .posts__title {
        text-align: center;
        margin-bottom: 15px;
    }
    .posts__title__desc{
        text-align: center;
        margin: 10px 0 25px;
        border-bottom: 2px solid #3e8969;
    }
</style>