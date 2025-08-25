---
title: redirect_to
description: This endpoint performs a 3xx redirect to a user-specified URL. It requires
  a `url` parameter, provided via query string or form data, to define the redirection
  target. An optional `status_code` parameter allows for specifying any valid 3xx
  status code, defaulting to 302 Found if not provided. Our implementation ensures
  the `Location` header is set to the exact, unmodified URL string supplied in the
  request.
openapi: GET, POST, PUT, DELETE, PATCH, TRACE ['/redirect-to']
---
# redirect_to

{% callout type="tip" %}
**Source:** [View on GitHub](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L576-L648)
{% /callout %}

{% callout type="tip" %}
**Source:** [View on GitHub](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L576-L648)

new callout
{% /callout %}

## Summary
This endpoint performs a 3xx redirect to a user-specified URL. It requires a `url` parameter, provided via query string or form data, to define the redirection target. An optional `status_code` parameter allows for specifying any valid 3xx status code, defaulting to 302 Found if not provided. Our implementation ensures the `Location` header is set to the exact, unmodified URL string supplied in the request.

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
`GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `TRACE`
{% /card %}
{% card title="Route Path" icon="route" %}
`/redirect-to`
{% /card %}
{% /cardGroup %}

## Usage Examples
{% codeGroup %}
```python {% title="Python" %}
import requests

params = {
    "url": "https://httpbin.org/get",
    "status_code": 302
}
response = requests.get("https://api.example.com/redirect-to", params=params, allow_redirects=False)
```

```javascript {% title="JavaScript" %}
fetch(`https://api.example.com/redirect-to?${new URLSearchParams({
  "url": "https://example.com/destination-page",
  "status_code": 302
})}`);
```

```java {% title="Java" %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newBuilder()
                .followRedirects(HttpClient.Redirect.NEVER)
                .build();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/redirect-to?url=https://httpbin.org/get&status_code=308"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println(response.statusCode());
        response.headers().firstValue("Location").ifPresent(System.out::println);
    }
}
```

```php {% title="PHP" %}
<?php

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/redirect-to?url=https%3A%2F%2Fexample.com&status_code=302");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, false);

$response = curl_exec($ch);

curl_close($ch);

echo $response;
```

```go {% title="Go" %}
package main

import (
	"fmt"
	"net/http"
	"net/url"
)

func main() {
	formData := url.Values{
		"url":         {"https://example.com"},
		"status_code": {"307"},
	}

	resp, err := http.PostForm("https://api.example.com/redirect-to", formData)
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()

	fmt.Println("Status Code:", resp.StatusCode)
	fmt.Println("Final URL:", resp.Request.URL)
}
```

```bash {% title="cURL" %}
curl -X GET "https://api.example.com/redirect-to?url=https%3A%2F%2Fexample.com&status_code=301"
```
{% /codeGroup %}

## Parameters
{% parameterField name="url" type="string" required=true %}
The URL to redirect to.
{% /parameterField %}

{% parameterField name="status_code" type="integer" default="302" %}
The HTTP status code to use for the redirect. This parameter is optional.
{% /parameterField %}

## Returns
`Response`: An object that represents an HTTP response.