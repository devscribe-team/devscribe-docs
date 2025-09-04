---
title: view_robots_page
description: This function serves the application's `robots.txt` file. It responds
  to GET requests at the `/robots.txt` endpoint by returning a predefined set of crawler
  directives with a `text/plain` content type.
openapi: GET ['/robots.txt']
---
# view_robots_page

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L266-L282)
{% /callout %}

## Summary
This function serves the application's `robots.txt` file. It responds to GET requests at the `/robots.txt` endpoint by returning a predefined set of crawler directives with a `text/plain` content type.

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
`GET`
{% /card %}
{% card title="Route Path" icon="route" %}
`/robots.txt`
{% /card %}
{% /cardGroup %}

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
`Response`: A Response object containing the 'robots.txt' rules with a 'text/plain' content type.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

url = "https://api.example.com/robots.txt"
response = requests.get(url)

print(f"Status Code: {response.status_code}")
print("Response Body:")
print(response.text)
```

```javascript {% title="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/robots.txt")
    .then(response => response.text())
    .then(data => console.log(data))
    .catch(error => console.error("Error:", error));
```

```java {% title="Java" showLineNumbers=true %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Example {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/robots.txt"))
                .GET()
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println(response.statusCode());
        System.out.println(response.body());
    }
}
```

```php {% title="PHP" showLineNumbers=true %}
<?php
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/robots.txt");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

$response = curl_exec($ch);

if(curl_errno($ch)){
    echo "cURL Error: " . curl_error($ch);
}

curl_close($ch);

print_r($response);
?>
```

```go {% title="GO" showLineNumbers=true %}
package main

import (
	"fmt"
	"io"
	"log"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/robots.txt")
	if err != nil {
		log.Fatalf("Error fetching URL: %v", err)
	}
	defer resp.Body.Close()

	if resp.StatusCode != http.StatusOK {
		log.Fatalf("Error: received status code %d", resp.StatusCode)
	}

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Fatalf("Error reading response body: %v", err)
	}

	fmt.Println(string(body))
}
```

```bash {% title="cURL" showLineNumbers=true %}
curl -X GET "https://api.example.com/robots.txt"
```
{% /codeGroup %}