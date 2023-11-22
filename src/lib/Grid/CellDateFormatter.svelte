<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let row;
    export let column;
    export let gridOptions

    function cellClickAction(cell, row, column) {
        let o = {
            cell,
            row,
            column,
            gridOptions
        }
        if(column.onCellClickHandler && column.onCellClickHandler != "") {
            o.onCellClickHandler = column.onCellClickHandler
        }
        dispatch("cellClicked", o);
    }
</script>


<td class="gridCellDateFormatter" on:click={cellClickAction(row[column.field], row, column)}>
    <span>
        {row[column.field] || ""}
    </span>
</td>

<style>
    .gridCellDateFormatter {
        border: 1px solid darkgrey;
        text-align: center;
    }

    .gridCellDateFormatter:hover {
        background-color: lightgreen;
    }
</style>