# Datatables

Datatables

Author

Benedict Thekkel

Sure! Here’s a streamlined guide on **Displaying Tables with DataTables Using Ajax and Fetch API**. This guide assumes you have your backend (e.g., Django DRF) already set up to provide the necessary data via API endpoints.

------------------------------------------------------------------------

## 1. **Include DataTables Assets**

First, ensure you include jQuery and DataTables CSS/JS in your HTML.

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>DataTables Example</title>
    <!-- DataTables CSS -->
    <link rel="stylesheet" href="https://cdn.datatables.net/1.13.4/css/jquery.dataTables.min.css">
</head>
<body>
    <table id="exampleTable" class="display" style="width:100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Email</th>
                <th>Department</th>
            </tr>
        </thead>
        <tbody>
            <!-- Data will be populated here -->
        </tbody>
    </table>

    <!-- jQuery -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <!-- DataTables JS -->
    <script src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>
</body>
</html>
```

------------------------------------------------------------------------

## 2. **Using DataTables with jQuery Ajax**

DataTables natively supports Ajax using jQuery. Here’s how to set it up:

### **Initialize DataTables with Ajax**

``` javascript
<script>
$(document).ready(function() {
    $('#exampleTable').DataTable({
        "ajax": {
            "url": "/api/data/", // Your API endpoint
            "dataSrc": "" // Adjust based on your API response structure
        },
        "columns": [
            { "data": "id" },
            { "data": "name" },
            { "data": "email" },
            { "data": "department" }
        ]
    });
});
</script>
```

### **Explanation:**

- **`ajax.url`**: URL of your API endpoint.
- **`ajax.dataSrc`**: Key in your JSON response where data array is located. Use `""` if the data is the root array.
- **`columns`**: Define which data fields to display in each column.

------------------------------------------------------------------------

## 3. **Using DataTables with Fetch API**

While DataTables is optimized for jQuery’s Ajax, you can integrate it with the Fetch API using its API methods.

### **Fetch Data and Populate DataTables**

``` javascript
<script>
document.addEventListener('DOMContentLoaded', function() {
    fetch('/api/data/') // Your API endpoint
        .then(response => response.json())
        .then(data => {
            $('#exampleTable').DataTable({
                data: data, // Your data array
                columns: [
                    { data: 'id' },
                    { data: 'name' },
                    { data: 'email' },
                    { data: 'department' }
                ]
            });
        })
        .catch(error => console.error('Error fetching data:', error));
});
</script>
```

### **Explanation:**

- **Fetch Data**: Use the Fetch API to retrieve data from the API endpoint.
- **Initialize DataTables**: Pass the fetched data to DataTables during initialization.

------------------------------------------------------------------------

## 4. **Handling Data Formatting**

Ensure your API returns data in a format compatible with DataTables. Typically, an array of objects where each object represents a row.

### **Sample JSON Response:**

``` json
[
    {
        "id": 1,
        "name": "John Doe",
        "email": "john@example.com",
        "department": "Engineering"
    },
    {
        "id": 2,
        "name": "Jane Smith",
        "email": "jane@example.com",
        "department": "Marketing"
    }
]
```

------------------------------------------------------------------------

## 5. **Advanced: Server-Side Processing with Fetch API**

For large datasets, handle pagination, sorting, and searching on the server.

### **Modify Fetch Request with Parameters**

``` javascript
<script>
document.addEventListener('DOMContentLoaded', function() {
    const table = $('#exampleTable').DataTable({
        "processing": true,
        "serverSide": true,
        "ajax": function(data, callback, settings) {
            // Map DataTables parameters to your API
            const params = {
                search: data.search.value,
                order: data.order.map(order => ({
                    column: data.columns[order.column].data,
                    dir: order.dir
                })),
                start: data.start,
                length: data.length
            };

            fetch(`/api/data/?search=${params.search}&start=${params.start}&length=${params.length}`)
                .then(response => response.json())
                .then(json => {
                    callback({
                        recordsTotal: json.total, // Total records
                        recordsFiltered: json.filtered, // Records after filtering
                        data: json.results // Data array
                    });
                })
                .catch(error => console.error('Error fetching data:', error));
        },
        "columns": [
            { "data": "id" },
            { "data": "name" },
            { "data": "email" },
            { "data": "department" }
        ]
    });
});
</script>
```

### **Explanation:**

- **`serverSide: true`**: Enables server-side processing.
- **Custom `ajax` function**: Handles sending parameters and processing the response to fit DataTables’ expectations.
- **API Response**: Should include `total`, `filtered`, and `results` fields.

------------------------------------------------------------------------

## 6. **Styling and Responsiveness**

Enhance table appearance and ensure it adapts to different screen sizes.

### **Add Responsive Extension (Optional)**

``` html
<!-- DataTables Responsive CSS -->
<link rel="stylesheet" href="https://cdn.datatables.net/responsive/2.4.1/css/responsive.dataTables.min.css">
<!-- DataTables Responsive JS -->
<script src="https://cdn.datatables.net/responsive/2.4.1/js/dataTables.responsive.min.js"></script>
```

### **Initialize with Responsive Option**

``` javascript
$('#exampleTable').DataTable({
    "responsive": true,
    // ... other options
});
```

------------------------------------------------------------------------

## 7. **Adding Export Buttons (Optional)**

Allow users to export table data in various formats.

### **Include Buttons Extension**

``` html
<!-- DataTables Buttons CSS -->
<link rel="stylesheet" href="https://cdn.datatables.net/buttons/2.3.6/css/buttons.dataTables.min.css">
<!-- DataTables Buttons JS -->
<script src="https://cdn.datatables.net/buttons/2.3.6/js/dataTables.buttons.min.js"></script>
<script src="https://cdn.datatables.net/buttons/2.3.6/js/buttons.html5.min.js"></script>
<script src="https://cdn.datatables.net/buttons/2.3.6/js/buttons.print.min.js"></script>
```

### **Initialize with Buttons**

``` javascript
$('#exampleTable').DataTable({
    "dom": 'Bfrtip',
    "buttons": [
        'copy', 'csv', 'excel', 'pdf', 'print'
    ],
    // ... other options
});
```

------------------------------------------------------------------------

Back to top
