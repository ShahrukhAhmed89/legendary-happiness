<script>

	import Form from './components/Form.svelte';
	import ListItem from './components/ListItem.svelte';

	let showForm = false;

	let todoList = JSON.parse(localStorage.getItem("todoList")) || [],
		activeList = [];


	$: {
		activeList = todoList;
		filterList( activeTag )
	}

	let todoTags = ['all', 'outdoor', 'chore', 'work']

	function submitForm(e) {

		let data = e.detail;

		todoList = [...todoList, {
			title : data.title,
			date : data.date,
			time : data.time,
			tag : data.tag,
			description : data.description,
			isChecked : false,
			id: Math.round(Math.random() * 100000)
		}]
		
		showForm = false;
	}

	function deleteItem(e) {
		// const index = todoList.findIndex( item => item.id === e.detail.id );
		// todoList.splice( index, 1);
		// todoList = todoList;
		todoList = todoList.filter( item => item.id !== e.detail.id );

	}
	
	function checkForCheck(e) {
		const index = todoList.findIndex( item => item.id === e.detail.id )
		todoList[index].isChecked = e.detail.checked;
		todoList = todoList;
	}

	let activeTag = 'all'
	function filterList( tag ){
		activeTag = tag;
		if ( tag !== 'all' ){
			activeList = todoList.filter( item => item.tag === tag )
		}
		else {
			activeList = todoList;
		}
	}

	window.onunload = function() {
		localStorage.setItem('todoList', JSON.stringify(todoList));
	}
</script>


<div id="app">
	<div class="todo-list">
		<h1 class="app__header">
			Todo List
		</h1>
		<div class="btn-container">
			{#each todoTags as tag }
				<button on:click={ () => filterList(tag) } class:btn-active={ activeTag === tag }>{tag}</button>
			{/each }
		</div>
		<div class="lists_container">
			{#each activeList as activity }
				<ListItem {activity} on:deleteItem={ deleteItem } on:radioCheck={ checkForCheck }/>
			{:else }
				<p class="no-task-alert">No Tasks Added </p>
			{/each }

		</div>
	</div>
	<div class="button-container">
		<button class="open-modal" on:click={ () => showForm = true }>
			<svg width="60" height="60">
				<circle cx="30" cy="30" r="25"></circle>
				<line x1="20" x2="40" y1 ="30" y2="30"></line>
				<line x1="30" x2="30" y1 ="20" y2="40"></line>
			</svg>
		</button>
	</div>
</div>


{#if showForm }
	<Form on:formSubmit={ submitForm }/>
{/if }