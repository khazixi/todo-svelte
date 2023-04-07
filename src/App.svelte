<script lang="ts">
    let placeholder = ""
    let todoItems: Array<string> = []

    let todoHolder: editHolder = {
        msg: "",
        idx: 0,
        active: false,
    }

    type editHolder = {
        msg: string
        idx: number
        active: boolean
    }
</script>


<main>
    <p>{placeholder}</p>
    <ul>
        {#each todoItems as todoItem, todoIdx }
            <li> {todoItem} </li>
            <button
                on:click={() => {todoItems.splice(todoIdx, 1); todoItems = todoItems}}>
            Delete
            </button>

            <button
                on:click={() => {todoHolder.active = true; todoHolder.idx = todoIdx; todoHolder.msg = todoItem}}
            >
                Edit
            </button>
        {/each}
    </ul>
    <form action="submit" on:submit={e => e.preventDefault()}>
        <input type="text"  bind:value={placeholder}>
        <input type="submit" 
        on:click={() => { todoItems.push(placeholder); todoItems = todoItems; placeholder = ""} }
        name="Submission button">
    </form>

    {#if todoHolder.active}
        <form action="submit" on:submit={e => e.preventDefault()}>
            <input type="text"  bind:value={todoHolder.msg}>
            <input type="submit" 
            on:click={() => { todoItems[todoHolder.idx] = todoHolder.msg; todoItems = todoItems; todoHolder.msg = ""; todoHolder.active = false} }
            name="Submission button">
        </form>
    {/if}
</main>
