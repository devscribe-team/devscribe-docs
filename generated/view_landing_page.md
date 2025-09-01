---
title: view_landing_page
description: This function handles GET requests for the `/legacy` endpoint by rendering
  and returning the `index.html` template. This route provides a legacy layout for
  the application's main landing page.
openapi: GET ['/legacy']
---
# view_landing_page

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L240-L243)
{% /callout %}

## Summary
This function handles GET requests for the `/legacy` endpoint by rendering and returning the `index.html` template. This route provides a legacy layout for the application's main landing page.

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" description="" %}
`GET`
{% /card %}
{% card title="Route Path" icon="route" description="" %}
`/legacy`
{% /card %}
{% /cardGroup %}

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
`render_template`: The function returns a call to `render_template`, which is used to render a template into a response object.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

response = requests.get("https://api.example.com/legacy")

print(response.text)
```

```javascript {% title="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/legacy")
  .then(response => response.text())
  .then(html => console.log(html))
  .catch(error => console.error("Error:", error));
```

```java {% title="Java" showLineNumbers=true %}
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Example {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/legacy"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println(response.body());
    }
}
```

```php {% title="PHP" showLineNumbers=true %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.example.com/legacy",
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

```go {% title="GO" showLineNumbers=true %}
package main

import (
	"fmt"
	"io"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/legacy")
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}

	fmt.Println(string(body))
}
```

```bash {% title="cURL" showLineNumbers=true %}
curl "https://api.example.com/legacy"
```
{% /codeGroup %}