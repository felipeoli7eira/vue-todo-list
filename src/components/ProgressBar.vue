<template>
    <div class="progress-bar-container">
        <div class="progress-bar" :style="{width: percentage + '%'}"></div>
    </div>
</template>

<script>
    export default {

        props: {
            percentage: {
                type: Number,
                default: 0
            }
        }

    }
</script>

<style>

    .progress-bar-container
    {
        margin-bottom: 5px;
        width: 100%;
        height: 5px;
    }

    .progress-bar
    {
        height: 100%;
        background-color: #8bcea7;
    }
</style>