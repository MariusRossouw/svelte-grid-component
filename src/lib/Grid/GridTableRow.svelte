<script>
    import { createEventDispatcher } from "svelte";
    import GridTableRowColumn from "./GridTableRowColumn.svelte"

    const dispatch = createEventDispatcher();

    export let grid;
    export let role;

    function cellClickHandler(e) {
        dispatch("cellClicked", e.detail);
    }
</script>

{#each grid.rowData as row, rowIndex (rowIndex)}
    <tr class="gridRow" class:gridRowIsSelected={row.rowIndex > -1 && row.selected === true} style={"--height: " + grid.gridOptions.rowHeight}>
        <GridTableRowColumn {row} {rowIndex} {role} columnDefs={grid.columnDefs} gridOptions={grid.gridOptions} on:cellClick={cellClickHandler}/>
    </tr>
{/each}


<style>
    .gridRow {
        border: 1px solid grey;
        color: var(--primaryTextColor, black);
        height: var(--height, 30px);
    }

    .gridRow:hover {
        border: 1px solid darkgray;
        background-color: lightblue;
        color: var(--secondaryTextColor, pink);
    }

    .gridRowIsSelected {
        background-color: bisque;
    }
</style>