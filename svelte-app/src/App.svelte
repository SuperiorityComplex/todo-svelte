<script>
	let newTask = '';
	let todoList = [
		{task: 'Write script section for todo website', completed: true, id: Date.now()},
		{task: 'Write body of todo website', completed: false, id: Date.now()},
		{task: 'Add comments', completed: false, id: Date.now()}
	];
	
	const add = () => {
		newTask = newTask.trim();
		if (!newTask) return;
		todoList = [...todoList, {task: newTask, completed: false, id: Date.now()}];
		newItem = '';
	}
	
	const remove = (index) => {
		todoList.splice(index, 1)
		todoList = todoList;
	}
	
	const dateToInternalDate = x => {
		const d = new Date(x)
		return `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}-${String(d.getDate()).padStart(2, '0')}`
	}
</script>

<input bind:value={newTask} type="text" placeholder="Add todo task">
<button on:click={add}>Add task</button>

<br/>
{#each todoList as {task, completed, id}, index}
	<input bind:checked={completed} type="checkbox">
	<span class:checked={completed}>{task} (added: {dateToInternalDate(id)})</span>
	<button on:click={() => remove(index)}>Delete</button>
	<br/>
{/each} 


<style> 
	.checked {
		text-decoration: line-through;
		color: green;
	}
</style> 