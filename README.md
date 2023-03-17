# Bulk-screenshots-with-JSON-payload

import requests
import json
from PIL import Image
import io
import matplotlib.pyplot as plt

# Set up the request payload
payload = {
    "access_key": "<your access key>",
    "execute": True,
    "optimize": True,
    "options": {"url": "https://example.com", "viewport_width": 1280, "viewport_height": 1024},
    "requests": [
        {"viewport_width": 360, "viewport_height": 640},
        {"viewport_width": 736, "viewport_height": 414}
    ]
}

# Send the POST request with the payload
response = requests.post('https://api.screenshotone.com/bulk', json=payload)

# Parse the response content as JSON
response_json = json.loads(response.content)

# Check the status code of the response
status_code = response.status_code
if status_code != 200:
    print(f"Error: {status_code} - {response_json.get('error')}")
    # Handle the error in some way (retry, log, etc.)
else:
    # Access the screenshot URLs for each request in the response
    for request_data in response_json['data']:
        screenshot_urls = request_data['screenshot_urls']
        for screenshot_url in screenshot_urls:
            # Load the image from the URL
            response = requests.get(screenshot_url)
            img = Image.open(io.BytesIO(response.content))
            # Display the image using matplotlib
            plt.imshow(img)
            plt.show()
