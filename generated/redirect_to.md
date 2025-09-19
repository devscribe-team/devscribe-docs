---
title: redirect_to
description: ''
api: GET, POST, PUT, DELETE, PATCH, TRACE /redirect-to
---
## Summary
This endpoint issues a redirect to a user-provided URL. It accepts a `url` and an optional `status_code` from the request's query string or form data, depending on the HTTP method. For a successful redirection, a `status_code` within the 3xx range must be provided. The response's `Location` header is set to the exact `url` value supplied. If a valid 3xx status code is not provided, the endpoint returns a 400 Bad Request. This route handles GET, POST, PUT, DELETE, PATCH, and TRACE requests.

## Parameters
{% parameterField name="url" type="string" required=true %}
The URL to which the client should be redirected.
{% /parameterField %}

{% parameterField name="status_code" type="number" default="302" %}
The HTTP status code to use for the redirection.
{% /parameterField %}

## Returns
`Response`: An object that contains all the information, like status code and headers, that is sent back to a client in response to its request.

## Usage Examples
{% codeGroup %}

```python {% filename="Python" showLineNumbers=true %}
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

```javascript {% filename="JavaScript" showLineNumbers=true %}
const response = await fetch("https://api.example.com/redirect-to?url=https%3A%2F%2Fexample.com&status_code=302", {
  redirect: "manual"
});

console.log(response.status);
console.log(response.headers.get("Location"));
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
                .uri(URI.create("https://api.example.com/redirect-to?url=https://example.com&status_code=302"))
                .build();

        HttpResponse<Void> response = client.send(request, HttpResponse.BodyHandlers.discarding());

        int statusCode = response.statusCode();
        String location = response.headers().firstValue("Location").orElse("");

        System.out.println("Status Code: " + statusCode);
        System.out.println("Redirect Location: " + location);
    }
}

```

```php {% filename="PHP" showLineNumbers=true %}
<?php

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/redirect-to?url=https://example.org&status_code=302");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, false);

$response = curl_exec($ch);

curl_close($ch);

?>
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

	req, err := http.NewRequest("GET", "https://api.example.com/redirect-to?url=https://example.org&status_code=302", nil)
	if err != nil {
		panic(err)
	}

	resp, err := client.Do(req)
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()

	fmt.Printf("Status: %s\n", resp.Status)
	fmt.Printf("Location: %s\n", resp.Header.Get("Location"))
}

```

```bash {% filename="cURL" showLineNumbers=true %}
curl "https://api.example.com/redirect-to?url=https://httpbin.org/get&status_code=302"
```
{% /codeGroup %}

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L592-L665)
{% /callout %}