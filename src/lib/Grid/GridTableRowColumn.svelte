<script>
    import { createEventDispatcher } from "svelte";
    import Cell from "./Cell.svelte"
    import CellRenderer from "./CellRenderer.svelte"
    import CellDateFormatter from "./CellDateFormatter.svelte"
    import CellValueFormatter from "./CellValueFormatter.svelte"
    import CellCurrencyFormatter from "./CellCurrencyFormatter.svelte"

    const dispatch = createEventDispatcher();

    export let columnDefs;
    export let gridOptions;
    export let row
    export let rowIndex


    function cellClickHandler(e) {
        e.detail.rowIndex = rowIndex
        dispatch("cellClick", e.detail);
    }
</script>

{#each columnDefs as column, columnIndex (columnIndex)} 
    {#if column.cellRenderer}
        <CellRenderer {row} {column} {gridOptions} on:cellClicked={cellClickHandler}/>
    {:else if column.valueFormatter}
        <CellValueFormatter {row} {column} {gridOptions} on:cellClicked={cellClickHandler}/>
    {:else if column.dateFormatter}
        <CellDateFormatter {row} {column} {gridOptions} on:cellClicked={cellClickHandler}/>
    {:else if column.currencyFormatter}
        <CellCurrencyFormatter {row} {column} {gridOptions} on:cellClicked={cellClickHandler}/>
    {:else}
        <Cell {row} {column} {gridOptions} on:cellClicked={cellClickHandler}/>
    {/if}
{/each}

<style>

</style>