<template>
    <ul class="task-container">
        <template v-if="tasks.length">
            <Task
                v-for="(task, index) in tasks"
                :key="task.name"
                :task="task"
                @onEmit="$emit('onEmit', index)"
                @onToggleStateTask="$emit('onToggleStateTask', index)"
            />
        </template>
        <li class="no-task" v-else>Vida boa :)</li>
    </ul>
</template>

<script>

    import Task from "./Task.vue"

    export default {

        components: { Task },
        props: {
            tasks: { type: Array, required: true }
        }

    }

</script>

<style>

    ul.task-container
    {
        padding-top: 3rem;
        width: 100%;
    }

    li.no-task
    {
        list-style: none;
        text-transform: uppercase;
        font-size: 14px;
        font-weight: 600;
        text-align: center;
    }

</style>