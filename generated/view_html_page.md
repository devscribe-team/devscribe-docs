---
title: view_html_page
description: This API endpoint handles GET requests to the `/html` route, serving
  a simple HTML document. It renders a predefined static template, providing a basic
  `text/html` response for client testing purposes.
openapi: GET ['/html']
---
# view_html_page

{% callout type="tip" %}
**Source:** [View on GitHub](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L246-L259)
{% /callout %}

## Summary
This API endpoint handles GET requests to the `/html` route, serving a simple HTML document. It renders a predefined static template, providing a basic `text/html` response for client testing purposes.

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
GET
{% /card %}
{% card title="Route Path" icon="route" %}
`/html`
{% /card %}
{% /cardGroup %}

## Usage Examples
{% codeGroup %}
```python {% title="Python" %}
import requests

url = "https://api.example.com/html"
response = requests.get(url)

print(f"Status Code: {response.status_code}")
print(f"Content-Type: {response.headers['Content-Type']}")
print("Response Body:")
print(response.text)
```

```javascript {% title="JavaScript" %}
fetch("https://api.example.com/html")
  .then(response => response.text())
  .then(data => console.log(data))
  .catch(error => console.error("Error:", error));
```

```java {% title="Java" %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Example {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/html"))
                .header("Accept", "text/html")
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println(response.statusCode());
        System.out.println(response.body());
    }
}
```

```php {% title="PHP" %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.example.com/html",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
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

```go {% title="GO" %}
package main

import (
	"fmt"
	"io"
	"log"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/html")
	if err != nil {
		log.Fatalf("error making request: %s", err)
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Fatalf("error reading response body: %s", err)
	}

	fmt.Println(string(body))
}

```

```bash {% title="cURL" %}
curl -H "Accept: text/html" "https://api.example.com/html"
```
{% /codeGroup %}

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
`render_template()`: Renders a template from the template folder with the given context.