<script>
    import { createEventDispatcher } from 'svelte'
    import GridTableHeader from './GridTableHeader.svelte'
    import GridTableRow from './GridTableRow.svelte'
    import GridPagination from './GridPagination.svelte'

    const dispatch = createEventDispatcher()

    export let grid 
    export let role 
    export let showPagination

    function gridHeaderClicked(e) {
        dispatch('gridHeaderClick', 
        e.detail
        )
    }

    function cellClickedHandler(e) {
        dispatch("cellClick", e.detail);
    }

</script>

<div>
    <table>
        <!-- 
            The columns for the header row
         -->
         <thead>
            <GridTableHeader columnDefs={grid.columnDefs} {role} on:gridHeaderClick={gridHeaderClicked}/>
        </thead>
         <!-- 
            The table rows
          -->
        <tbody>
            <GridTableRow {grid} {role} on:cellClicked={cellClickedHandler}/>
        </tbody>
        <!-- 
        Pagination
     -->
     {#if showPagination}
        <div class="pagination">
            <GridPagination />
        </div>
     {/if}
    </table>
    
     
</div>

<style>
table {
    border-collapse: collapse;
    font-family: Roboto, Roboto Light, RobotoBlack, system-ui, -apple-system, BlinkMacSystemFont, 'Helvetica Neue', sans-serif;
    color: #222;
    background-color: #F6F7F8;
    font-size: 14px;
    margin: 0px;
    padding: 0px;
    border-spacing: 0;
    width: 100%;
    table-layout: fixed;
}
thead {
    position: sticky;
    z-index: 100;
    top: 0;
    -webkit-box-shadow:inset 0px 0px 0px 1px #000;
    -moz-box-shadow:inset 0px 0px 0px 1px #000;
    box-shadow:inset 0px 0px 0px 1px #000;
}

.pagination{
    position: sticky;
    z-index: 100;
    bottom: 0;
    left: 0;
    background: aquamarine;
    width: 100%;
    height: 30px;
    -webkit-box-shadow:inset 0px 0px 0px 1px #000;
    -moz-box-shadow:inset 0px 0px 0px 1px #000;
    box-shadow:inset 0px 0px 0px 1px #000;
}
</style>