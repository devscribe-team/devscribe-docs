---
title: view_landing_page
description: This endpoint, available at the `/legacy` route, is responsible for generating
  our legacy landing page by rendering and returning the `index.html` template.
openapi: GET ['/legacy']
---
# view_landing_page

{% callout type="tip" %}
**Source:** [View on GitHub](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L240-L243)
{% /callout %}

## Summary
This endpoint, available at the `/legacy` route, is responsible for generating our legacy landing page by rendering and returning the `index.html` template. modification

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
`GET`
{% /card %}
{% card title="Route Path" icon="route" %}
`/legacy`
{% /card %}
{% /cardGroup %}

## Usage Examples
{% codeGroup %}
```python {% title="Python" %}
import requests

url = "https://api.example.com/legacy"
response = requests.get(url)

print(response.status_code)
print(response.text)
```

```javascript {% title="JavaScript" %}
fetch("https://api.example.com/legacy")
  .then(response => response.text())
  .then(html => console.log(html))
  .catch(error => console.error("Error:", error));
```

```java {% title="Java" %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Main {
    public static void main(String[] args) {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/legacy"))
                .build();
        try {
            HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
            System.out.println(response.body());
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```php {% title="PHP" %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.example.com/legacy",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_CUSTOMREQUEST => "GET",
]);

$response = curl_exec($curl);

curl_close($curl);

echo $response;
```

```go {% title="Go" %}
package main

import (
	"fmt"
	"io"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/legacy")
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		panic(err)
	}

	fmt.Println(string(body))
}
```

```bash {% title="cURL" %}
curl -X GET "https://api.example.com/legacy"
```
{% /codeGroup %}

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
`render_template`: Renders a template from the templates folder.