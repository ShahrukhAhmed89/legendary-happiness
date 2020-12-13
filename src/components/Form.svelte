
<script>

    import { createEventDispatcher } from 'svelte';

    let todoTags = ['outdoor', 'chore', 'work'];

    const date = new Date();

    let formTitle = '',
        formDate = `${date.getFullYear()}-${date.getMonth() + 1}-${date.getDate()}`,
        formTime = `${("0" + date.getHours()).slice(-2)}:${("0" + date.getMinutes()).slice(-2)}`,
        formTag,
        formDescription = '';


    const dispatch = createEventDispatcher();

    function submitForm(e){
        e.preventDefault();
        dispatch('formSubmit', {
            title : formTitle,
			date : formDate,
			time : formTime,
			tag : formTag,
			description : formDescription
        })
    }
</script>

<div class="modal-background">
    <div class="form-modal">
        <h2>Add Task</h2>
        <form class="form" id="formElement">
            <div class="input-container">
                <label for="task-title">Task Name</label>
                <input id="task-title" type="text" name="taskName" placeholder="Enter Task Title" bind:value={ formTitle }>
            </div>
            <div class="input-container">
                <label for="task-date">Date</label>
                <input type="date" name="taskDate" id="task-date" bind:value={ formDate }>
            </div>
            <div class="input-container">
                <label for="task-time">Time</label>
                <input type="time" name="taskTime" id="task-time" bind:value={ formTime }>
            </div>

            <div class="input-container">
                <label for="task-tag">Tag</label>
                <select name="taskTag" id="task-tag" bind:value={ formTag }>
                    {#each todoTags as tag }
                        <option value="{tag}">{tag}</option>
                    {/each }
                </select>
            </div>
            <div class="input-container">
                <label for="task-description">Task Description</label>
                <textarea name="taskDescription" id="task-description" bind:value={ formDescription }></textarea>
            </div>
            
            <div class="input-container">
                <input type="submit" value="Sumbit" id="form-button" on:click="{ submitForm }">
            </div>
        </form>
    </div>
</div>


<!-- <div class="modal-background">
    <div class="form-modal">
        <h2>Add Task</h2>
        <form class="form" id="formElement">
            <div class="input-container">
                <label for="task-title">Task Name</label>
                <input id="task-title" type="text" name="taskName" placeholder="Enter Task Title" bind:value={ formTitle }>
            </div>
            <div class="input-container">
                <label for="task-date">Date</label>
                <input type="date" name="taskDate" id="task-date" bind:value={ formDate }>
            </div>
            <div class="input-container">
                <label for="task-time">Time</label>
                <input type="time" name="taskTime" id="task-time" bind:value={ formTime }>
            </div>

            <div class="input-container">
                <label for="task-tag">Tag</label>
                <select name="taskTag" id="task-tag" bind:value={ formTag }>
                    {#each todoTags as tag }
                        <option value="{tag}">{tag}</option>
                    {/each }
                </select>
            </div>
            <div class="input-container">
                <label for="task-description">Task Description</label>
                <textarea name="taskDescription" id="task-description" bind:value={ formDescription }></textarea>
            </div>
            
            <div class="input-container">
                <input type="submit" value="Sumbit" id="form-button" on:click="{ submitForm }">
            </div>
        </form>
    </div>
</div> -->