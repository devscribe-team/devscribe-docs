---
title: redirect_n_times
description: "This endpoint initiates a sequence of `n` HTTP 302 redirects. The nature\
  \ of these redirects\u2014whether they use absolute or relative URLs\u2014is determined\
  \ by the `absolute` query parameter. If `absolute` is set to `true`, the entire\
  \ chain of redirects will use absolute URLs. The final redirect in the sequence\
  \ always resolves to the `/get` endpoint."
openapi: GET ['/redirect/<int:n>']
---
# redirect_n_times

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L541-L567)
{% /callout %}

## Summary
This endpoint initiates a sequence of `n` HTTP 302 redirects. The nature of these redirects—whether they use absolute or relative URLs—is determined by the `absolute` query parameter. If `absolute` is set to `true`, the entire chain of redirects will use absolute URLs. The final redirect in the sequence always resolves to the `/get` endpoint.

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
The number of times to redirect.
{% /parameterField %}

{% parameterField name="absolute" type="boolean" default="false" %}
An optional query parameter that determines if the redirect URL is absolute.
{% /parameterField %}

## Returns
`redirect` or `_redirect`: The function returns a call to either the `redirect` or `_redirect` function, both of which construct and return an HTTP redirect response.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

response = requests.get("https://api.example.com/redirect/5", allow_redirects=True)

print(f"Final destination URL: {response.url}")
print(f"Status code: {response.status_code}")
```

```javascript {% title="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/redirect/5")
    .then(response => response.text())
    .then(html => console.log(html))
    .catch(error => console.error("Error:", error));
```

```java {% title="Java" showLineNumbers=true %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class ApiClient {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newBuilder()
                .followRedirects(HttpClient.Redirect.ALWAYS)
                .build();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/redirect/3"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println("Final Status Code: " + response.statusCode());
        System.out.println("Final URI: " + response.uri());
    }
}
```

```php {% title="PHP" showLineNumbers=true %}
<?php

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/redirect/5");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
curl_setopt($ch, CURLOPT_MAXREDIRS, 5);

$response = curl_exec($ch);

curl_close($ch);

echo $response;

```

```go {% title="GO" showLineNumbers=true %}
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

	req, err := http.NewRequest("GET", "https://api.example.com/redirect/5", nil)
	if err != nil {
		fmt.Println(err)
		return
	}

	resp, err := client.Do(req)
	if err != nil {
		fmt.Println(err)
		return
	}
	defer resp.Body.Close()

	fmt.Printf("Status: %s\n", resp.Status)

	location, err := resp.Location()
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Printf("Redirect Location: %s\n", location)
}
```

```bash {% title="cURL" showLineNumbers=true %}
curl -L "https://api.example.com/redirect/3?absolute=true"
```
{% /codeGroup %}