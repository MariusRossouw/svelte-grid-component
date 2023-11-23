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


<td class="gridCellRenderer" on:click={() => cellClickAction(row[column.field], row, column)}>
    <span>
        {@html column.cellRenderer  || ""}
    </span>
</td>


<style>
    .gridCellRenderer {
        display:flex;
        align-items:center;
        justify-content:center;
    }

    .gridCellRenderer:hover {
        background-color: transparent;
    }

    /* td:first-child {
        position: sticky;
        left: 0;
        background: darkgrey;
        z-index: 100;
    } */
</style>