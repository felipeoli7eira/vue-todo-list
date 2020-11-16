<template>
<li class="task" :class="stateClass" @click="$emit('onToggleStateTask', task)">
    <span> {{ task.name }} </span>
    <span @click.stop="$emit('onEmit', task)" class="close"></span>
</li>
</template>

<script>

    export default {

        props: {
            task: { type: Object, required: true }
        },

        computed: {
            stateClass()
            {
                return {
                    pending: this.task.pending,
                    done: !this.task.pending
                }
            }
        }
    }

</script>

<style>

    li.task
    {
        list-style: none;
        cursor: pointer;
        user-select: none;
        border-radius: 3px;
        font-weight: 500;
        padding: 10px;
        margin-bottom: 10px;
        border: 1px solid #f1f1f1;
        background-color: #f5f5f5;
        display: flex;
        justify-content: space-between;
    }

    .task span.close
    {
        transition: all 0.2s;
        width: 20px;
        text-align: center;
        border-radius: 20px;
        height: 20px;
        background-color: #696969;
    }

    .task span.close:hover
    {
        background-color: #464646;
    }

    .task.pending
    {
        background-color: #fd837a;
        color: #65322e;
    }

    .task.done
    {
        background-color: #8bcea7;
        color: #1c4629;
        text-decoration: line-through;
    }

</style>