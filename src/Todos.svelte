<script>
    import { fly } from 'svelte/transition';
    let todoItem = '';
    let todoList = [];

    //ADD ITEMS FROM INPUT TO ARRAY

    function addToList (){
        todoList = [...todoList, {
            text: todoItem,
            status: false
        }];
        todoItem='';
    }

    //REMOVE ITEMS FROM INPUT TO ARRAY

    function removeFromList(index){
        todoList.splice(index, 1);
        todoList= todoList;
    }

	
    
</script>

<form on:submit|preventDefault={addToList}>
    <input bind:value={todoItem}>
</form>

<ul class="todo-list">
    {#each todoList as item, index}
    <li transition:fly={{y: 20, duration: 200}}>
    <input bind:checked={item.status} class="check" type='checkbox'>
    <span class:checked={item.status}>{item.text}</span>
    <button class="delete" type="button" on:click={() =>removeFromList(index)}></button>
    </li>

    {/each}
</ul>

<style>
    .todo-list{
        color: rgb(0, 204, 255);
		font-family: 'American Typewriter', condensed;
		font-size: 2em;
    }
    .checked{
        text-decoration: line-through;
    }
</style>