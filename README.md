# Dynamic Date Display

This HTML code provides a way to display dynamic date or time information based on a specified `modified-date` attribute. It calculates the time difference between the current date and the provided `modified-date` and displays the appropriate text.

## Usage

To use this code, follow these steps:

1. Include the provided HTML code in your web page.
2. Add elements with the class `date-or-time` where you want to display the dynamic date or time information.
3. Set the `modified-date` attribute on each `date-or-time` element with the desired date or time value in the format `YYYY-MM-DDTHH:mm:ssZ` (e.g., `2024-06-19T19:32:00+05:30`).

Javascript Code:
```javascript
    document.addEventListener("DOMContentLoaded", function () {
      var dateElements = document.querySelectorAll('.date-or-time');

      dateElements.forEach(function (dateOrTimeElement) {
        var dateAttributeValue = dateOrTimeElement.getAttribute('modified-date');
        var dateToDisplay = dateAttributeValue ? new Date(dateAttributeValue) : null;

        // Only display if a valid date is available
        if (dateToDisplay && !isNaN(dateToDisplay.getTime())) {
          // Calculate the time difference in seconds
          var now = new Date();
          var timeDifference = Math.floor((now - dateToDisplay) / 1000);

          // Calculate minutes, hours, days
          var minutes = Math.floor(timeDifference / 60);
          var hours = Math.floor(minutes / 60);
          var days = Math.floor(hours / 24);

          // Display dynamic content based on time difference
          if (minutes < 60) {
            dateOrTimeElement.textContent = minutes + " minute" + (minutes !== 1 ? "s" : "") + " ago";
          } else if (hours < 24) {
            dateOrTimeElement.textContent = hours + " hour" + (hours !== 1 ? "s" : "") + " ago";
          } else if (days === 1) {
            dateOrTimeElement.textContent = "Yesterday";
          } else if (days <= 6) {
            dateOrTimeElement.textContent = days + " day" + (days !== 1 ? "s" : "") + " ago";
          } else {
            // Display date in the format like "23 Nov 2023"
            dateOrTimeElement.textContent = dateToDisplay.toLocaleString('en-us', { day: 'numeric', month: 'short', year: 'numeric' });
          }
        } else {
          // If the date is invalid or missing, hide the element
          dateOrTimeElement.style.display = 'none';
        }
      });
    });
```
Example:
```html
<div class="date-or-time" modified-date="2024-06-19T19:32:00+05:30">2023-12-03</div>
<span class="date-or-time" modified-date="2023-12-03T19:12:00+05:30">2023-12-03</span>
```

## How It Works

The code uses JavaScript to dynamically update the content of elements with the class `date-or-time` based on the `modified-date` attribute value. Here's how it works:

1. The script waits for the DOM content to be loaded using the `DOMContentLoaded` event listener.
2. It selects all elements with the class `date-or-time` using `document.querySelectorAll('.date-or-time')`.
3. For each `date-or-time` element:
   - It retrieves the value of the `modified-date` attribute.
   - It parses the date value using `new Date(dateAttributeValue)`.
   - If the parsed date is valid, it calculates the time difference between the current date and the parsed date in seconds.
   - Based on the time difference, it determines the appropriate text to display:
     - If the difference is less than 60 minutes, it displays "X minute(s) ago".
     - If the difference is less than 24 hours, it displays "X hour(s) ago".
     - If the difference is exactly 1 day, it displays "Yesterday".
     - If the difference is less than or equal to 6 days, it displays "X day(s) ago".
     - If the difference is more than 6 days, it displays the date in the format "DD MMM YYYY".
   - If the parsed date is invalid or missing, the element is hidden using `display: none;`.
