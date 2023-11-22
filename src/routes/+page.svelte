<script>
    import Grid from "$lib/Grid/Grid.svelte"

    let role = "ALL"

    let selectedRow = {}

    let selectedRows = []

    let grid = {
        gridOptions: {
            onRowClick: true,
            onRowClickHandler: "openRow"
        },
        columnDefs: [
            {headerName: "First Name", field: "first_name", onCellClickHandler: "openRow", roles: ["Super Admin","Operator"], width: "200px"},
            {headerName: "Last Name", field: "last_name", roles: ["Super Admin","Operator"], width: "200px"},
            {headerName: "Date", field: "date", roles: ["Super Admin","Operator"], dateFormatter: "yyy-mm-d", width: "200px"},
            {headerName: "Amount", field: "amount", roles: ["Super Admin"], currencyFormatter: ["en-US", "ZAR", "narrowSymbol", false, "ZAR"], width: "200px"},
            {headerName: "Size", field: "size", roles: ["Super Admin"], valueFormatter: ["en-US", "centimeter", "short", false, "centimeters"], width: "200px"},
            {headerName: "Open", field: "open", roles: ["Super Admin"], onCellClickHandler: "openRow", cellRenderer: "<button style='cursor: pointer'>Open</button>", width: "80px"},
            {headerName: "Single Select", field: "single_select", roles: ["Super Admin","Operator"], onCellClickHandler: "singleSelect", width: "50px"},
            {headerName: "Multi Select", field: "multi_select", roles: ["Super Admin","Operator"], onCellClickHandler: "multiSelect", width: "50px"}
        ],
        rowData: [
            {first_name: "Marius", last_name: "Rossouw", amount:1259.88, size:1259.88, date: "2023-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "2023/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:1259.88, size:1259.88, date: "2023-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "2023/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:1259.88, size:1259.88, date: "2023-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "2023/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:1259.88, size:1259.88, date: "2023-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "2023/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:1259.88, size:1259.88, date: "2023-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "2023/07/11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982-07-11"},
            {first_name: "Marius", last_name: "Rossouw", amount:129.88, size:1259.88, date: "1982/07/11"}
        ]
    }

    function onGridHeaderClickHandler(e) {
        console.log('Column header clicked: ', e.detail)
    }

    function onCellClickHandler(e) {
        console.log("Cell Click Event in Page: ", e.detail)
        if(e.detail.onCellClickHandler) {
        let handler = e.detail.onCellClickHandler;
            // window[fn](handler);
            if(handler === 'openRow') {
                openRow(e.detail)
            }
            if(handler === 'singleSelect') {
                singleSelect(e.detail)
            }
            if(handler === 'multiSelect') {
                multiSelect(e.detail)
            }
        }
    }

    function openRow(params) {
        console.log('openRow Function: ', params)
    }

    function singleSelect(params) {
        selectedRow = {}
        console.log('singleSelect Function: ', params)
        selectedRow = grid.rowData[params.rowIndex]
    }

    function multiSelect(params) {
        console.log('multiSelect Function: ', params)
        if(grid.rowData[params.rowIndex].selected) {
            grid.rowData[params.rowIndex].selected = false
            for(let i = 0; i < selectedRows.length; i++) {
                if(selectedRows[i].rowIndex == params.rowIndex) {
                    selectedRows.splice(i, 1);
                    selectedRows = [...selectedRows];
                }
            }
        } else {
            grid.rowData[params.rowIndex].selected = true;
            grid.rowData[params.rowIndex].rowIndex = params.rowIndex;
            selectedRows = [...selectedRows, grid.rowData[params.rowIndex]]
        }
    }

</script>

<h1>Grid</h1>
<div style="width:100%; height:300px; overflow: auto;">
    <Grid {grid} {role} on:gridHeaderClick={onGridHeaderClickHandler} on:cellClick={onCellClickHandler} />
</div>


<pre>
    <code>
        {JSON.stringify(grid.rowData, null, 2)}
    </code>
</pre>

<pre>
    <code>
        {JSON.stringify(selectedRow, null, 2)}
    </code>
</pre>

<pre>
    <code>
        {JSON.stringify(selectedRows, null, 2)}
    </code>
</pre>
