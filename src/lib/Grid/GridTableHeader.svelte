<script>
    import { createEventDispatcher } from 'svelte'
    import GridTableHeaderCell from "./GridTableHeaderCell.svelte"

    const dispatch = createEventDispatcher()

    export let columnDefs 
    export let role 

    function gridHeaderClicked(e) {
        dispatch('gridHeaderClick', e.detail)
    }

</script>

{#each columnDefs as column, index (index)}
    {#if (column.roles && column.roles.indexOf(role) > -1) || role === 'ALL'}
        <GridTableHeaderCell {column} {index} on:gridHeaderClick={gridHeaderClicked}/>
    {/if}
{/each}
