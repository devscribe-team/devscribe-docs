---
title: redirect_to
description: ''
api: GET , POST , PUT , DELETE , PATCH , TRACE /redirect-to
num: 1
---
## Summary
This endpoint issues a redirect to a user-specified URL. It requires a `url` parameter and accepts an optional `status_code` parameter, both provided in the request's query string. The response's `Location` header is set to the exact string value of the `url` parameter without any modification. The `status_code` parameter must be a valid 3xx redirection code to control the response's status. If a valid redirection status code is not provided, the endpoint returns a 400 Bad Request.

## Parameters
{% parameterField name="url" type="string" required=true %}
The target URL for the redirection.
{% /parameterField %}

{% parameterField name="status_code" type="integer" %}
An optional integer that specifies the HTTP redirect status code (e.g., 302, 307).
{% /parameterField %}

## Returns
`Response`: An object that represents an HTTP response in Flask.

## Usage Examples
{% codeGroup %}

```python {% filename="Python" showLineNumbers=true %}
import requests

url = "https://api.example.com/redirect-to"
params = {
    "url": "https://example.org",
    "status_code": 302
}

response = requests.get(url, params=params, allow_redirects=False)

print(f"Status Code: {response.status_code}")
if "Location" in response.headers:
    print(f"Redirects to: {response.headers['Location']}")

```

```javascript {% filename="JavaScript" showLineNumbers=true %}
async function redirectToExample() {
  const response = await fetch("https://api.example.com/redirect-to?url=https%3A%2F%2Fexample.com&status_code=302", {
    redirect: "manual"
  });

  console.log(response.status);
  console.log(response.headers.get("Location"));
}

redirectToExample();
```

```java {% filename="Java" showLineNumbers=true %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class RedirectExample {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newBuilder()
                .followRedirects(HttpClient.Redirect.NEVER)
                .build();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/redirect-to?url=https://example.com/destination&status_code=302"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println("Status Code: " + response.statusCode());
        response.headers().firstValue("Location").ifPresent(location -> System.out.println("Location Header: " + location));
    }
}
```

```php {% filename="PHP" showLineNumbers=true %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
    CURLOPT_URL => "https://api.example.com/redirect-to?url=https%3A%2F%2Fexample.com&status_code=302",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_FOLLOWLOCATION => false,
    CURLOPT_CUSTOMREQUEST => "GET",
]);

$response = curl_exec($curl);

curl_close($curl);

echo $response;
```

```go {% filename="GO" showLineNumbers=true %}
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

	req, err := http.NewRequest("GET", "https://api.example.com/redirect-to?url=https://httpbingo.org&status_code=302", nil)
	if err != nil {
		fmt.Println("Error creating request:", err)
		return
	}

	resp, err := client.Do(req)
	if err != nil {
		fmt.Println("Error sending request:", err)
		return
	}
	defer resp.Body.Close()

	fmt.Printf("Status Code: %d\n", resp.StatusCode)

	location, err := resp.Location()
	if err != nil {
		fmt.Println("Error getting location:", err)
		return
	}
	fmt.Printf("Redirect Location: %s\n", location)
}

```

```bash {% filename="cURL" showLineNumbers=true %}
curl "https://api.example.com/redirect-to?url=https://example.com/destination&status_code=302"
```
{% /codeGroup %}

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L592-L666)
{% /callout %}