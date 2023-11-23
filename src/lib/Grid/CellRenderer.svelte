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


<td class="gridCellRenderer" class:sticky={column.stickyPosition > -1} style={"--index: "+column.stickyPosition+"; --width: "+column.width} on:click={() => cellClickAction(row[column.field], row, column)}>
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

    .sticky {
        position: sticky;
        left: calc(var(--index)*var(--width));
        background: lightblue;
        z-index: 99;
    }
</style>