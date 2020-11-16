<template>
    <div class="new-task-form">
        <input v-model="name" type="text" @keydown.enter="add" autofocus>
        <button @click="add">add</button>
    </div>
</template>

<script>

    export default {

        data()
        {
            return {
                name: ""
            }
        },

        methods:
        {
            add()
            {
                this.$emit("onEmit", { name: this.name })
                this.name = ""
            }
        }

    }

</script>

<style>

    .new-task-form
    {
        width: 100%;
        display: flex;
        justify-content: space-between;
    }

    .new-task-form input, .new-task-form button
    {
        outline: none;
        border: none;
        background: none;
        border-radius: 2px;
        padding: 15px;
    }

    .new-task-form input
    {
        border: 1px solid #f2f2f2;
        flex-grow: 1;
    }

    .new-task-form button
    {
        font-weight: 600;
        color: #ffffff;
        cursor: pointer;
        transition: all 0.2s;
        background-color: #60866d;
    }

    .new-task-form button:hover
    {
        background-color: #79a889;
    }
</style>