---
title: view_robots_page
description: This function serves the `robots.txt` file, providing a standard set
  of rules for web crawlers. It responds to GET requests at the `/robots.txt` endpoint
  by returning the predefined rules with a `text/plain` content type.
openapi: GET ['/robots.txt']
---
# view_robots_page

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L266-L282)
{% /callout %}

## Summary
This function serves the `robots.txt` file, providing a standard set of rules for web crawlers. It responds to GET requests at the `/robots.txt` endpoint by returning the predefined rules with a `text/plain` content type.

## API Info
{% cardGroup cols=2 gap="sm" %}
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
`make_response`: A Flask helper function that creates a Response object.

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

public class RobotsExample {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/robots.txt"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println("Status Code: " + response.statusCode());
        System.out.println("Response Body: " + response.body());
    }
}
```

```php {% title="PHP" showLineNumbers=true %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.example.com/robots.txt",
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

```go {% title="Go" showLineNumbers=true %}
package main

import (
	"fmt"
	"io"
	"net/http"
	"os"
)

func main() {
	resp, err := http.Get("https://api.example.com/robots.txt")
	if err != nil {
		fmt.Fprintf(os.Stderr, "failed to get robots.txt: %v\n", err)
		os.Exit(1)
	}
	defer resp.Body.Close()

	if resp.StatusCode != http.StatusOK {
		fmt.Fprintf(os.Stderr, "unexpected status code: %d\n", resp.StatusCode)
		os.Exit(1)
	}

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		fmt.Fprintf(os.Stderr, "failed to read response body: %v\n", err)
		os.Exit(1)
	}

	fmt.Println(string(body))
}
```

```bash {% title="cURL" showLineNumbers=true %}
curl "https://api.example.com/robots.txt"
```
{% /codeGroup %}