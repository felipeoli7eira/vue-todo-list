<template>
	<main id="app">
		<ProgressBar :percentage="percentage" />
		<NewTaskForm @onEmit="addTask" />
		<TaskGrid
			:tasks="tasks"
			@onEmit="deleteTask"
			@onToggleStateTask="toggleStateTask"
		/>
	</main>
</template>

<script>

import ProgressBar from "./components/ProgressBar.vue"
import TaskGrid from "./components/TaskGrid.vue"
import NewTaskForm from "./components/NewTaskForm.vue"

export default {

	components: { TaskGrid, NewTaskForm, ProgressBar },

	data()
	{
		return {
			tasks: []
		}
	},

	watch: {

		tasks: {
			deep: true,
			handler()
			{
				localStorage.tasks = JSON.stringify(this.tasks)
			}
		}

	},

	computed: {
		percentage()
		{
			let totalTasks = this.tasks.length
			let completedTasks = this.tasks.filter((task) => !task.pending).length

			return Math.round( completedTasks / totalTasks * 100 ) || 0
		}
	},

	methods: {

		addTask(props)
		{
			let isNewTask = this.tasks.filter( (task) => {
				return task.name === props.name
			} ).length === 0

			if(isNewTask)
			{  
				this.tasks.push(
					{
						name: props.name,
						pending: props.pending || true
					}
				)
				document.querySelector("input").focus()

				return true
			}

			document.querySelector("input").focus()

			return false
		},

		deleteTask(taskIndex)
		{
			this.tasks.splice(taskIndex, 1)
		},

		toggleStateTask(index)
		{
			this.tasks[index].pending = !this.tasks[index].pending
		}
	},

	created()
	{
		let jsonTasks = localStorage.tasks
		this.tasks = JSON.parse( jsonTasks ) || []
	}

}
</script>

<style>
	*
	{
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		font-family: "Montserrat";
	}

	#app
	{
		max-width: 600px;
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		align-items: center;

		padding: 2rem 1rem;
	}
</style>
