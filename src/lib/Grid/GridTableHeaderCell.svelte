<script>
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher()

    export let column 
    // export let gridOptions
    // export let role

    

    function gridHeaderClicked(column) {
        dispatch('gridHeaderClick', column)
    }

</script>

<th class="gridHeader" style={"width:"+column.width} on:click={() => gridHeaderClicked(column)}>
    <span>
        {column.headerName}
    </span>
</th>

<style>
    .gridHeader {
        background-color: aquamarine;
        border: 1px solid darkgrey;
        
    }

    .gridHeader:hover {
        border: 1px solid darkgray;
        background-color: lightblue;
    }
</style>