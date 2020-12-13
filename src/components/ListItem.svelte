
<script>
    import { createEventDispatcher } from 'svelte';
    import { fade } from 'svelte/transition';

    const dispatch = createEventDispatcher();

    export let activity;

    function deleteItem(){
        dispatch('deleteItem', {
            id : activity.id
        })
    }

    function checkForCheck(e){
        dispatch('radioCheck', {
            id : activity.id,
            checked: e.target.checked
        })
    }
</script>


<div class="list__container">
    <input 
        type="checkbox" 
        id="item-list-{ activity.id }" 
        data-id="{ activity.id }" 
        checked={ activity.isChecked } 
        on:click={ checkForCheck } >

    <label for="item-list-{activity.id}">
        <div class="list__content">
            <h2>{ activity.title }</h2>
            <time datetime="{ activity.date } { activity.time }">
                <span>{ activity.date }</span>
                <span>{ activity.time }</span>
            </time>
            <p>
                { activity.description }
            </p>
        </div>
    </label>
    <button class="delete-item" on:click={ deleteItem }> X </button>
</div>