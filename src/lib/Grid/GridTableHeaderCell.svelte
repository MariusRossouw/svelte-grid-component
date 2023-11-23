<script>
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher()

    export let column 
    export let index
    // export let gridOptions
    // export let role

    

    function gridHeaderClicked(column) {
        dispatch('gridHeaderClick', column)
    }

</script>

<th class="gridHeader" class:sticky={column.sticky} style={"width: "+column.width+"; --index: "+column.stickyPosition+"; --width: "+column.width} on:click={() => gridHeaderClicked(column)}>
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

    .sticky {
        position: sticky;
        left: calc(var(--index)*var(--width));
        background: lightblue;
        z-index: 99;
    }
</style>