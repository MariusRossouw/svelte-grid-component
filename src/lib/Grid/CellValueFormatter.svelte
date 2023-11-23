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

    function format(number, locale, unit, unitDisplay, onlyValue, removeItem) {
        // locale -> "en-GB", "ja-JP", "en-US"
        // unit -> "kilometer-per-hour", "liter"
        // unitDisplay -> "long", "short", "narrow"
        // onlyValue -> true, false
        // removeItem -> what ever should be removed from the string
        // https://v8.dev/features/intl-numberformat
        let c = new Intl.NumberFormat(locale, {
            style: "unit",
            unit,
            unitDisplay
        })
            .format(number)
            .trim();
        
        if(onlyValue === true) {
            c = c.replace(removeItem, "").trim();
        }

        return c
    }

    // console.log("Test1: ", format(12345, "en-US", "centimeter", "long", false, "centimeters"))
    // console.log("Test2: ", format(12345, "en-US", "centimeter", "short", false, "centimeters"))
    // console.log("Test3: ", format(12345, "en-US", "centimeter", "narrow", false, "centimeters"))
    // console.log("Test4: ", format(12345, "en-US", "centimeter", "long", false, "centimeters"))
    // console.log("Test5: ", format(12345, "en-US", "centimeter", "long", true, "centimeters"))
    // console.log("Test6: ", format(12345, "en-US", "centimeter", "short", true, "cm"))
    // console.log("Test7: ", format(12345, "en-US", "centimeter", "narrow", true, "cm"))
</script>

<td class="gridCellValueFormatter" class:sticky={column.sticky} style={"--index: "+column.stickyPosition+"; --width: "+column.width} on:click={cellClickAction(row[column.field], row, column)}>
    <span>
        {#if column.valueFormatter && column.valueFormatter.length > 0}
            {format(row[column.field],...column.valueFormatter) || ""}
        {/if}
    </span>
</td>

<style>
    .gridCellValueFormatter {
        border: 1px solid darkgrey;
        text-align: right;
        padding-right: 10px;
    }

    .gridCellValueFormatter:hover {
        background-color: lightpink;
    }

    .sticky {
        position: sticky;
        left: calc(var(--index)*var(--width));
        background: lightblue;
        z-index: 99;
    }
</style>