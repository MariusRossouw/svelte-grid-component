<script>
    import { onMount } from "svelte";
    import {writable} from "svelte/store"
    import {setContext} from "svelte"
    import { createEventDispatcher } from 'svelte'
    import GridTable from "./GridTable.svelte"

    const dispatch = createEventDispatcher()

    export let role = 'ALL';
    export let showPagination = true
    export let grid = {
        gridOptions: {},
        columnDefs: [],
        rowData: []
    };
    export let gridName = crypto.randomUUID()

    onMount(() => {
        
    });

    function gridHeaderClickHandler(e) {
        dispatch('gridHeaderClick', e.detail)
    }

    function cellckickHandler(e) {
        dispatch('cellClick', e.detail)
    }

</script>

<div>
    <GridTable {grid} {role} {gridName} {showPagination} on:gridHeaderClick={gridHeaderClickHandler} on:cellClick={cellckickHandler}/>
</div>
