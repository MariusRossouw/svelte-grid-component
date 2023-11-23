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


<td class="gridCell" class:sticky={column.stickyPosition > -1} style={"--index: "+column.stickyPosition+"; --width: "+column.width} on:click={cellClickAction(row[column.field], row, column)}>
    <span>
        {row[column.field] || ""}
    </span>
</td>

<style>
    .gridCell {
        border: 1px solid darkgrey;
        text-align: center;
    }

    .gridCell:hover {
        background-color: lavender;
    }

    .sticky {
        position: sticky;
        left: calc(var(--index)*var(--width));
        background: lightblue;
        z-index: 99;
    }
</style>