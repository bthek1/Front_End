# Google Analytics

Google Analytics (GA) helps track website traffic, user behavior, and performance. Integrating it into a Django project allows for better insights into user interactions.

Author

Benedict Thekkel

# **Google Analytics in a Django Project: Complete Guide**

------------------------------------------------------------------------

## **1. Setting Up Google Analytics**

### **Step 1: Create a Google Analytics Account**

1.  Go to [Google Analytics](https://analytics.google.com/analytics/web/)
2.  Click **Admin** \> **Create Account** \> **Create Property**
3.  Choose **GA4 (Google Analytics 4)**
4.  Set up a new **Web Stream** and copy the **Measurement ID** (format: `G-XXXXXXXXXX`)

------------------------------------------------------------------------

## **2. Adding Google Analytics to Django**

### **Option 1: Adding Google Analytics Script in HTML**

1.  Open your base template (`base.html`):

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>My Django App</title>
    <script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
    <script>
      window.dataLayer = window.dataLayer || [];
      function gtag(){dataLayer.push(arguments);}
      gtag('js', new Date());

      gtag('config', 'G-XXXXXXXXXX');
    </script>
</head>
<body>
    {% block content %}{% endblock %}
</body>
</html>
```

Replace `G-XXXXXXXXXX` with your **Google Analytics Measurement ID**.

2.  Reload the page and check **Google Analytics Real-Time Dashboard**.

### **Option 2: Dynamic Google Analytics ID in Django Settings**

Instead of hardcoding the ID, you can use Django settings.

1.  **In `settings.py`**:

``` python
GOOGLE_ANALYTICS_ID = "G-XXXXXXXXXX"
```

2.  **In `base.html`**:

``` html
{% if GOOGLE_ANALYTICS_ID %}
<script async src="https://www.googletagmanager.com/gtag/js?id={{ GOOGLE_ANALYTICS_ID }}"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', '{{ GOOGLE_ANALYTICS_ID }}');
</script>
{% endif %}
```

3.  **Modify `context_processors.py`**:

``` python
def google_analytics(request):
    from django.conf import settings
    return {"GOOGLE_ANALYTICS_ID": getattr(settings, "GOOGLE_ANALYTICS_ID", "")}
```

4.  **Add context processor in `settings.py`**:

``` python
TEMPLATES = [
    {
        "OPTIONS": {
            "context_processors": [
                "your_project.context_processors.google_analytics",
            ],
        },
    },
]
```

Now, Django dynamically injects the Google Analytics ID.

------------------------------------------------------------------------

## **3. Tracking Custom Events**

Google Analytics allows you to track specific user actions.

### **Example: Tracking Button Clicks**

``` html
<button onclick="gtag('event', 'button_click', {'event_category': 'User Actions', 'event_label': 'Signup Button'});">
    Sign Up
</button>
```

Now, this event will appear in **Google Analytics \> Events**.

### **Tracking Page Views**

Google Analytics automatically tracks page views, but if using AJAX-based navigation, manually track:

``` html
<script>
  gtag('config', '{{ GOOGLE_ANALYTICS_ID }}', {'page_path': '{{ request.path }}'});
</script>
```

------------------------------------------------------------------------

## **4. Google Tag Manager Integration**

Google Tag Manager (GTM) allows you to manage GA and other tracking scripts in one place.

1.  **Get GTM Container ID** (e.g., `GTM-XXXXXXX`)
2.  **Add this to `base.html`**:

``` html
<head>
    <script async src="https://www.googletagmanager.com/gtm.js?id=GTM-XXXXXXX"></script>
</head>
<body>
    <noscript>
        <iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX"
                height="0" width="0" style="display:none;visibility:hidden"></iframe>
    </noscript>
</body>
```

Now, manage tracking via **Google Tag Manager** instead of editing HTML.

------------------------------------------------------------------------

## **5. Tracking Logged-in Users in Django**

To track authenticated users:

``` html
<script>
  gtag('set', {'user_id': '{{ request.user.id }}'}); 
</script>
```

This enables user tracking in **Google Analytics \> User Explorer**.

------------------------------------------------------------------------

## **6. Monitoring Performance (LCP, FID, CLS)**

To track **Core Web Vitals**:

``` html
<script>
  gtag('event', 'LCP', {'event_category': 'Performance', 'value': 2.5});
  gtag('event', 'FID', {'event_category': 'Performance', 'value': 0.1});
  gtag('event', 'CLS', {'event_category': 'Performance', 'value': 0.03});
</script>
```

View results under **GA \> Reports \> Performance**.

------------------------------------------------------------------------

## **7. Google Analytics in Django Admin**

If you want to track **admin panel usage**, add:

``` html
{% if request.user.is_staff %}
<script>
  gtag('config', '{{ GOOGLE_ANALYTICS_ID }}', {'user_id': '{{ request.user.id }}', 'custom_dimension': 'admin_user'});
</script>
{% endif %}
```

Now, admin activity is logged separately.

------------------------------------------------------------------------

## **8. Testing & Debugging**

### **Google Tag Assistant Extension**

- Install [Tag Assistant](https://chrome.google.com/webstore/detail/tag-assistant/kejbdjndbnbjgmefkgdddjlbokphdefk)
- Check if GA is loading correctly.

### **GA Debug Mode**

``` html
<script>
  gtag('config', 'G-XXXXXXXXXX', {'debug_mode': true});
</script>
```

### **Real-Time Monitoring**

Go to **Google Analytics \> Reports \> Realtime**.

------------------------------------------------------------------------

## **9. Server-Side Tracking with Django**

Instead of client-side tracking, send analytics data via Django views.

### **Example: Track API Events**

``` python
import requests

GA_ENDPOINT = "https://www.google-analytics.com/mp/collect"
GA_ID = "G-XXXXXXXXXX"
GA_SECRET = "YOUR_MEASUREMENT_PROTOCOL_SECRET"

def track_event(event_name, user_id=None):
    payload = {
        "client_id": user_id or "anonymous",
        "events": [{"name": event_name}]
    }
    headers = {"Content-Type": "application/json"}
    requests.post(f"{GA_ENDPOINT}?measurement_id={GA_ID}&api_secret={GA_SECRET}", json=payload, headers=headers)

# Usage
track_event("user_logged_in", user_id="12345")
```

Now, backend events can be tracked without JavaScript.

------------------------------------------------------------------------

## **10. Comparing Django Analytics Tools**

| Feature             | Google Analytics | Django Debug Toolbar | Matomo |
|---------------------|------------------|----------------------|--------|
| User Tracking       | ✅ Yes           | ❌ No                | ✅ Yes |
| Pageviews           | ✅ Yes           | ✅ Yes               | ✅ Yes |
| Event Tracking      | ✅ Yes           | ❌ No                | ✅ Yes |
| Requires JavaScript | ✅ Yes           | ❌ No                | ❌ No  |
| GDPR Compliant      | ❌ No            | ✅ Yes               | ✅ Yes |

For privacy-focused apps, consider **Matomo** (self-hosted).

------------------------------------------------------------------------

## **Conclusion**

✔ **Basic Tracking**: Add GA script in `base.html`\
✔ **Custom Events**: Track clicks, logins, form submissions\
✔ **Google Tag Manager**: Manage tracking codes centrally\
✔ **Authenticated Users**: Send user IDs to GA\
✔ **Server-Side Tracking**: Use Django views for analytics

Now, your Django app is fully integrated with **Google Analytics**! 🚀

------------------------------------------------------------------------

Back to top
