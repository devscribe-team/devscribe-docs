---
title: redirect_n_times
description: This endpoint initiates a sequence of `n` HTTP 302 redirects, where `n`
  is an integer specified in the URL path. The redirects are relative by default but
  can be made absolute by setting the `absolute` query parameter to `true`. After
  `n-1` redirects, the final redirect in the chain resolves to the `/get` endpoint.
openapi: GET ['/redirect/<int:n>']
---
# redirect_n_times

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L541-L567)
{% /callout %}

## Summary
This endpoint initiates a sequence of `n` HTTP 302 redirects, where `n` is an integer specified in the URL path. The redirects are relative by default but can be made absolute by setting the `absolute` query parameter to `true`. After `n-1` redirects, the final redirect in the chain resolves to the `/get` endpoint.

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
`GET`
{% /card %}
{% card title="Route Path" icon="route" %}
`/redirect/<int:n>`
{% /card %}
{% /cardGroup %}

## Parameters
{% parameterField name="n" type="integer" required=true %}
An integer that specifies the number of times to redirect.
{% /parameterField %}
{% parameterField name="absolute" type="boolean" default="false" %}
An optional query parameter that specifies whether the redirect URL is absolute.
{% /parameterField %}

## Returns
`redirect or _redirect`: Returns a function call to either `redirect()` or `_redirect()`, which both generate an HTTP redirect response.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

response = requests.get("https://api.example.com/redirect/5", allow_redirects=False)

print(response.status_code)
print(response.headers["Location"])
```
```javascript {% title="JavaScript" showLineNumbers=true %}
async function followRedirects() {
  const response = await fetch("https://api.example.com/redirect/5");
  const data = await response.text();
  console.log(data);
}

followRedirects();
```
```java {% title="Java" showLineNumbers=true %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class RedirectExample {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newBuilder()
                .followRedirects(HttpClient.Redirect.ALWAYS)
                .build();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/redirect/5"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println("Final Status Code: " + response.statusCode());
        System.out.println("Final URL: " + response.uri());
    }
}
```
```php {% title="PHP" showLineNumbers=true %}
<?php

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/redirect/5");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);

$response = curl_exec($ch);

curl_close($ch);

echo $response;

?>
```
```go {% title="Go" showLineNumbers=true %}
package main

import (
	"fmt"
	"log"
	"net/http"
)

func main() {
	client := &http.Client{
		CheckRedirect: func(req *http.Request, via []*http.Request) error {
			return http.ErrUseLastResponse
		},
	}

	req, err := http.NewRequest("GET", "https://api.example.com/redirect/5", nil)
	if err != nil {
		log.Fatalf("Error creating request: %v", err)
	}

	resp, err := client.Do(req)
	if err != nil {
		log.Fatalf("Error sending request: %v", err)
	}
	defer resp.Body.Close()

	fmt.Printf("Status Code: %d\n", resp.StatusCode)

	location, err := resp.Location()
	if err != nil {
		log.Fatalf("Error getting location: %v", err)
	}
	fmt.Printf("Redirect Location: %s\n", location)
}
```
```bash {% title="cURL" showLineNumbers=true %}
curl "https://api.example.com/redirect/3?absolute=true"
```
{% /codeGroup %}