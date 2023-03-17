# Bulk-screenshots-with-JSON-payload
Bulk screenshots with JSON payload, python and https://screenshotone.com api
This code first sends the POST request with the payload to the API endpoint using the requests.post() method, 
then parses the response content as JSON using json.loads(). 
It then checks the HTTP status code of the response to determine whether the request was successful or not. If the status code is not 200, it prints an error message (and optionally handles the error in some way). 
Otherwise, it loops over each request in the response and extracts the screenshot URLs for that request from the response JSON object. 
For each screenshot URL, it sends a GET request to download the image data, loads the image data into a Pillow Image object, and displays the image using matplotlib.
