# High Charts

To use **Highcharts** in a Django REST Framework (DRF) project, you need to integrate Highcharts on the frontend with Django and DRF on the backend. The general workflow involves the following steps:

Author

Benedict Thekkel

## 1. **Setting Up a Django DRF Project**

### a. Install Django and Django REST Framework

First, set up your Django project and install the necessary dependencies:

``` bash
pip install django djangorestframework
```

Create a new Django project and app:

``` bash
django-admin startproject myproject
cd myproject
python manage.py startapp charts
```

Add the following to `INSTALLED_APPS` in `myproject/settings.py`:

``` python
INSTALLED_APPS = [
    # other apps
    'rest_framework',
    'charts',  # your new app
]
```

### b. Create a Model to Store Chart Data

In the `charts/models.py`, define a model that holds the data you want to visualize using Highcharts. For example, let’s create a model for sales data:

``` python
from django.db import models

class SalesData(models.Model):
    date = models.DateField()
    revenue = models.DecimalField(max_digits=10, decimal_places=2)

    def __str__(self):
        return f"{self.date}: {self.revenue}"
```

### c. Create a Serializer for the Data

In `charts/serializers.py`, create a serializer to convert the `SalesData` model into JSON format:

``` python
from rest_framework import serializers
from .models import SalesData

class SalesDataSerializer(serializers.ModelSerializer):
    class Meta:
        model = SalesData
        fields = ['date', 'revenue']
```

### d. Create a View to Provide the Data as an API

In `charts/views.py`, create an API view that fetches and returns the sales data:

``` python
from rest_framework import generics
from .models import SalesData
from .serializers import SalesDataSerializer

class SalesDataList(generics.ListAPIView):
    queryset = SalesData.objects.all()
    serializer_class = SalesDataSerializer
```

### e. Set Up the URL for the API

In `charts/urls.py`, create a route for the API view:

``` python
from django.urls import path
from .views import SalesDataList

urlpatterns = [
    path('sales/', SalesDataList.as_view(), name='sales-data'),
]
```

In your main `myproject/urls.py`, include the `charts` app URLs:

``` python
from django.urls import path, include

urlpatterns = [
    # other URLs
    path('api/', include('charts.urls')),
]
```

### f. Migrate and Create Sample Data

Run the migrations and create some sample data for testing:

``` bash
python manage.py makemigrations
python manage.py migrate
```

In the Django admin or shell, create a few `SalesData` records for testing.

------------------------------------------------------------------------

## 2. **Frontend Integration: Highcharts Setup**

Once you have the Django DRF API serving data, you can set up Highcharts on the frontend to visualize it.

### a. Setting Up Highcharts in a Django Template

In the `charts/templates/charts/index.html` file, include Highcharts via CDN and fetch data using JavaScript. For example:

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sales Data</title>
    <script src="https://code.highcharts.com/highcharts.js"></script>
    <script src="https://code.highcharts.com/modules/exporting.js"></script>
</head>
<body>
    <div id="container"></div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            fetch('/api/sales/')
                .then(response => response.json())
                .then(data => {
                    const categories = data.map(item => item.date);
                    const revenues = data.map(item => parseFloat(item.revenue));

                    Highcharts.chart('container', {
                        chart: {
                            type: 'line'
                        },
                        title: {
                            text: 'Sales Revenue Over Time'
                        },
                        xAxis: {
                            categories: categories
                        },
                        yAxis: {
                            title: {
                                text: 'Revenue (USD)'
                            }
                        },
                        series: [{
                            name: 'Revenue',
                            data: revenues
                        }]
                    });
                });
        });
    </script>
</body>
</html>
```

### b. Serving the Template

In `charts/views.py`, create a view to serve the HTML page that contains the Highcharts:

``` python
from django.shortcuts import render

def index(request):
    return render(request, 'charts/index.html')
```

Update `charts/urls.py` to serve this view:

``` python
from django.urls import path
from .views import SalesDataList, index

urlpatterns = [
    path('sales/', SalesDataList.as_view(), name='sales-data'),
    path('', index, name='index'),
]
```

------------------------------------------------------------------------

## 3. **Handling Data from Django DRF in Highcharts**

When fetching data from Django DRF, you often deal with JSON arrays or objects. Highcharts requires the data to be processed into a specific format.

### Example of Mapping API Data to Highcharts

``` javascript
fetch('/api/sales/')
    .then(response => response.json())
    .then(data => {
        const categories = data.map(item => item.date);
        const revenues = data.map(item => parseFloat(item.revenue));

        Highcharts.chart('container', {
            chart: {
                type: 'column'  // Type of chart
            },
            title: {
                text: 'Monthly Sales Revenue'
            },
            xAxis: {
                categories: categories
            },
            yAxis: {
                title: {
                    text: 'Revenue (USD)'
                }
            },
            series: [{
                name: 'Revenue',
                data: revenues
            }]
        });
    });
```

------------------------------------------------------------------------

## 4. **Customizing Highcharts in Django Projects**

### a. Customizing Chart Types

You can change the chart type (e.g., line, column, pie) by modifying the `chart.type` property. Highcharts supports multiple chart types, such as `line`, `bar`, `pie`, `scatter`, and more.

Example:

``` javascript
chart: {
    type: 'bar'  // Bar chart instead of a line chart
}
```

### b. Adding Tooltips and Data Labels

You can add **tooltips** and **data labels** for better interactivity and user experience:

``` javascript
tooltip: {
    pointFormat: '{series.name}: <b>{point.y:.2f}</b><br/>',
    valueSuffix: ' USD'
},
plotOptions: {
    series: {
        dataLabels: {
            enabled: true,
            format: '{point.y:.2f}'
        }
    }
}
```

### c. Handling Time Series Data

If you’re working with time series data (e.g., date-based data), you can configure the x-axis to be a datetime axis:

``` javascript
xAxis: {
    type: 'datetime',
    categories: data.map(item => new Date(item.date).getTime()),  // Convert dates to timestamps
    labels: {
        format: '{value:%Y-%m-%d}'  // Format the date labels
    }
}
```

------------------------------------------------------------------------

## 5. **Real-Time Updates in Highcharts with DRF**

To update Highcharts in real-time, you can either use: - **Polling**: Periodically fetch new data from the DRF API using JavaScript `setInterval`. - **WebSockets**: Use Django Channels to push real-time updates to the frontend.

### Example: Polling Data for Real-Time Updates

``` javascript
setInterval(() => {
    fetch('/api/sales/')
        .then(response => response.json())
        .then(data => {
            const categories = data.map(item => item.date);
            const revenues = data.map(item => parseFloat(item.revenue));

            const chart = Highcharts.chart('container', {
                series: [{
                    data: revenues
                }],
                xAxis: {
                    categories: categories
                }
            });
            chart.redraw();  // Update the chart with new data
        });
}, 5000);  // Fetch new data every 5 seconds
```

------------------------------------------------------------------------

## 6. **Exporting Charts**

Highcharts has built-in support for exporting charts as **PNG**, **JPEG**, **PDF**, or **SVG**. You can enable exporting by including the `exporting.js` module and adding export buttons.

### Example:

``` javascript
<script src="https://code.highcharts.com/modules/exporting.js"></script>

Highcharts.chart('container', {
    exporting: {
        enabled: true  // Adds export buttons for saving chart as PNG, PDF, etc.
    }
});
```

------------------------------------------------------------------------

## 7. **Common Highcharts Modules**

Highcharts provides several additional modules that you can include in your Django DRF project: - **Highcharts Stock**: For financial and stock charts. - **Highcharts Maps**: For visualizing geographical data. - **Highcharts Gantt**: For Gantt charts and project management timelines.

Include these as separate modules:

``` html
<script src="https://code.highcharts.com/stock/highstock.js"></script>
<script src="https://code.highcharts.com/maps/modules/map

.js"></script>
```

------------------------------------------------------------------------

## Recommanded Data Structure from DRF with Ajax with Fetch API

> When working with Django REST Framework (DRF) and sending data for use with **Highcharts** (a popular charting library) via **AJAX using Fetch API**, the structure of your JSON response from the DRF API must be properly formatted to match the expected data structure for Highcharts.

------------------------------------------------------------------------

### Recommended JSON Structure for Highcharts Series Chart

Highcharts accepts a specific format for its data, particularly for series-based charts (e.g., line charts, column charts). Here’s a general overview of the JSON structure for **series** data in Highcharts:

``` json
{
  "chart": {
    "type": "line"  // Chart type (e.g., 'line', 'column', etc.)
  },
  "title": {
    "text": "Example Chart Title"
  },
  "xAxis": {
    "categories": ["Jan", "Feb", "Mar", "Apr", "May"]  // Labels for X-axis
  },
  "series": [
    {
      "name": "Series 1",
      "data": [29.9, 71.5, 106.4, 129.2, 144.0]  // Data points for Series 1
    },
    {
      "name": "Series 2",
      "data": [34.9, 68.5, 98.4, 124.2, 145.0]  // Data points for Series 2
    }
  ]
}
```

For a typical **line or column chart** in Highcharts, you will need to return two main pieces of data: 1. **Categories (X-axis)**: A list of values representing the categories (e.g., months, days, time points). 2. **Series (Y-axis)**: An array of objects where each object represents a series of data points with a `name` (label for the series) and `data` (the actual data points).

### Example DRF JSON Response

Your DRF view should return a similar JSON structure that can be easily consumed by the front-end JavaScript using the Fetch API. Here’s how you might structure the JSON in your Django view:

``` json
{
  "chart_type": "line",  // Optional: Provide chart type from the backend
  "categories": ["Jan", "Feb", "Mar", "Apr", "May"],  // X-axis categories
  "series": [
    {
      "name": "Series 1",
      "data": [29.9, 71.5, 106.4, 129.2, 144.0]  // Y-axis data points for Series 1
    },
    {
      "name": "Series 2",
      "data": [34.9, 68.5, 98.4, 124.2, 145.0]  // Y-axis data points for Series 2
    }
  ]
}
```

### Example Django DRF View

Here’s how you can set up your Django view to return this data:

``` python
from rest_framework.response import Response
from rest_framework.views import APIView

class HighchartsDataView(APIView):
    def get(self, request, *args, **kwargs):
        data = {
            "chart_type": "line",
            "categories": ["Jan", "Feb", "Mar", "Apr", "May"],
            "series": [
                {
                    "name": "Series 1",
                    "data": [29.9, 71.5, 106.4, 129.2, 144.0]
                },
                {
                    "name": "Series 2",
                    "data": [34.9, 68.5, 98.4, 124.2, 145.0]
                }
            ]
        }
        return Response(data)
```

### Example JavaScript Fetch API to Fetch and Use Data in Highcharts

On the front-end, you can use the **Fetch API** to request data from your DRF API and use it to render a Highcharts chart:

``` javascript
document.addEventListener('DOMContentLoaded', function () {
  fetch('http://localhost:8000/api/highcharts-data/')
    .then(response => response.json())
    .then(data => {
      Highcharts.chart('container', {
        chart: {
          type: data.chart_type  // Dynamic chart type from API
        },
        title: {
          text: 'Django DRF Highcharts Example'
        },
        xAxis: {
          categories: data.categories  // X-axis categories from API
        },
        series: data.series  // Series data from API
      });
    })
    .catch(error => console.error('Error fetching data:', error));
});
```

### Points to Consider:

1.  **Dynamic Data**: The data in your DRF response could be dynamically generated based on queries (e.g., fetching data from a database). You should ensure the `categories` (X-axis) and `series` data are generated correctly.

2.  **Chart Customization**: You can also return additional chart customization options (such as the `chart_type` or title) from the DRF API if the chart configuration needs to be dynamic.

3.  **Efficient Data Transfer**: Depending on the size of your data, you may want to optimize the payload size (e.g., avoid sending unnecessary data or compress responses).

4.  **CORS**: If your front end is hosted separately from your Django API, ensure that **CORS** is correctly configured to allow the front-end application to access your API.

5.  **Authentication**: If your API is protected (e.g., requiring authentication), make sure you handle token-based or session-based authentication in your AJAX requests.

### Conclusion

For a typical Highcharts series chart in a Django DRF project, the JSON structure should include: - **categories** (for the X-axis). - **series** (an array of objects containing series names and data points).

By following this structure, you can easily integrate your Django DRF back end with a Highcharts front end using the Fetch API to retrieve data asynchronously.

Back to top
