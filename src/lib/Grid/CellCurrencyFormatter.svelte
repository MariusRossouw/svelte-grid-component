<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let row;
    export let column;
    export let gridOptions;

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

    function format(number, locale, currency, currencyDisplay, onlyValue, removeItem) {
        // locale -> "en-GB", "ja-JP", "en-US"
        // currency -> "ZAR", "USD", "EUR"
        // currencyDisplay -> "narrowSymbol", "symbol", "name", "code"
        // onlyValue -> true, false
        // removeItem -> what ever should be removed from the string "ZAR", "R"
        let c = new Intl.NumberFormat(locale, {
            style: "currency",
            currency,
            currencyDisplay
        })
            .format(number)
            .trim();
        
        if(onlyValue === true) {
            c = c.replace(removeItem, "").trim();
        }

        return c
    }

    // console.log("Test1: ", format(12345.67, "en-US", "ZAR", "code", false, "ZAR"))
    // console.log("Test2: ", format(12345, "en-US", "ZAR", "name", false, "ZAR"))
    // console.log("Test3: ", format(12345, "en-US", "ZAR", "symbol", false, "ZAR"))
    // console.log("Test4: ", format(12345, "en-US", "ZAR", "narrowSymbol", false, "ZAR"))
    // console.log("Test5: ", format(12345, "en-US", "ZAR", "code", true, "ZAR"))
    // console.log("Test6: ", format(12345, "en-US", "ZAR", "narrowSymbol", true, "R"))
    // console.log("Test7: ", format(12345, "en-US", "ZAR", "name", true, "South African rand"))
    
</script>

<td class="gridCellCurrencyFormatter" class:sticky={column.stickyPosition > -1} style={"--index: "+column.stickyPosition+"; --width: "+column.width} on:click={cellClickAction(row[column.field], row, column)}>
    <span>
        {#if column.currencyFormatter && column.currencyFormatter.length > 0}
            {format(row[column.field],...column.currencyFormatter) || ""}
        {/if}
    </span>
</td>

<style>
    .gridCellCurrencyFormatter {
        border: 1px solid darkgrey;
        text-align: right;
        padding-right: 10px;
    }

    .gridCellCurrencyFormatter:hover {
        background-color: lightcoral;
    }

    .sticky {
        position: sticky;
        left: calc(var(--index)*var(--width));
        background: lightblue;
        z-index: 99;
    }
</style>
