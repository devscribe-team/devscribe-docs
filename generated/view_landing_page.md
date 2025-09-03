---
title: view_landing_page
description: This function serves as the endpoint for the `/legacy` route. It renders
  and returns the `index.html` template, which displays the landing page in its legacy
  layout.
openapi: GET ['/legacy']
---
# view_landing_page

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L240-L243)
{% /callout %}

## Summary
This function serves as the endpoint for the `/legacy` route. It renders and returns the `index.html` template, which displays the landing page in its legacy layout.

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
`GET`
{% /card %}
{% card title="Route Path" icon="route" %}
`/legacy`
{% /card %}
{% /cardGroup %}

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
`render_template`: Renders a Jinja2 template to an HTML string.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

url = "https://api.example.com/legacy"
response = requests.get(url)

print(response.text)
```
```javascript {% title="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/legacy", {
    method: "GET"
})
.then(response => response.text())
.then(data => console.log(data))
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
                .GET()
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
	"log"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/legacy")
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
```bash {% title="cURL" showLineNumbers=true %}
curl "https://api.example.com/legacy"
```
{% /codeGroup %}