---
title: redirect_to
description: This endpoint redirects to a user-specified URL, accepting the target
  via an `url` parameter in either the query string or form data. It supports GET,
  POST, PUT, DELETE, PATCH, and TRACE methods. An optional `status_code` parameter
  can be provided to set a specific 3xx redirect code for the response. The `Location`
  header is set to the exact URL string supplied by the client, preserving its original
  form.
openapi: GET, POST, PUT, DELETE, PATCH, TRACE ['/redirect-to']
---
# redirect_to

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L591-L668)
{% /callout %}

## Summary
This endpoint redirects to a user-specified URL, accepting the target via an `url` parameter in either the query string or form data. It supports GET, POST, PUT, DELETE, PATCH, and TRACE methods. An optional `status_code` parameter can be provided to set a specific 3xx redirect code for the response. The `Location` header is set to the exact URL string supplied by the client, preserving its original form.

## API Info
{% cardGroup cols=2 gap="sm" %}
{% card title="HTTP Methods" icon="server" %}
`GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `TRACE`
{% /card %}
{% card title="Route Path" icon="route" %}
`/redirect-to`
{% /card %}
{% /cardGroup %}

## Parameters
{% parameterField name="url" type="string" required=true %}
The target URL for the redirection.
{% /parameterField %}
{% parameterField name="status_code" type="integer" %}
An optional integer representing the HTTP status code for the redirect.
{% /parameterField %}

## Returns
`Response`: A `Response` object that represents an HTTP response.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

url = "https://api.example.com/redirect-to"
params = {
    "url": "https://httpbin.org/get",
    "status_code": 302
}

response = requests.get(url, params=params, allow_redirects=False)

print(f"Status Code: {response.status_code}")
print(f"Location Header: {response.headers['Location']}")
```
```javascript {% title="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/redirect-to?url=https%3A%2F%2Fgoogle.com&status_code=302", {
  method: "GET"
});
```
```java {% title="Java" showLineNumbers=true %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class ApiClient {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newBuilder()
                .followRedirects(HttpClient.Redirect.NEVER)
                .build();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/redirect-to?url=https://example.com/new-page&status_code=302"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
    }
}
```
```php {% title="PHP" showLineNumbers=true %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.example.com/redirect-to?url=https://google.com&status_code=302",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_FOLLOWLOCATION => false,
]);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```
```go {% title="Go" showLineNumbers=true %}
package main

import (
	"fmt"
	"net/http"
)

func main() {
	client := &http.Client{
		CheckRedirect: func(req *http.Request, via []*http.Request) error {
			return http.ErrUseLastResponse
		},
	}

	req, err := http.NewRequest("GET", "https://api.example.com/redirect-to?url=https://example.org&status_code=302", nil)
	if err != nil {
		fmt.Println(err)
		return
	}

	resp, err := client.Do(req)
	if err != nil {
		fmt.Println(err)
		return
	}
	defer resp.Body.Close()

	fmt.Printf("Status Code: %d\n", resp.StatusCode)
	location, err := resp.Location()
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Printf("Location: %s\n", location)
}
```
```bash {% title="cURL" showLineNumbers=true %}
curl "https://api.example.com/redirect-to?url=https://httpbin.org/get&status_code=302"
```
{% /codeGroup %}