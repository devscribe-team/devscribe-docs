---
title: redirect_n_times
description: This endpoint initiates a sequence of `n` HTTP 302 redirects, where `n`
  is an integer specified in the URL path. The final redirect in the chain resolves
  to the `/get` endpoint. A boolean query parameter, `absolute`, can be provided to
  control whether the intermediate redirects use absolute or relative URLs.
openapi: GET ['/redirect/<int:n>']
---
# Header 1

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L541-L567)
{% /callout %}

## Summary
This endpoint initiates a sequence of `n` HTTP 302 redirects, where `n` is an integer specified in the URL path. The final redirect in the chain resolves to the `/get` endpoint. A boolean query parameter, `absolute`, can be provided to control whether the intermediate redirects use absolute or relative URLs.

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

{% parameterField name="absolute" type="boolean" %}
An optional query parameter that makes the redirection absolute. Defaults to `false`.
{% /parameterField %}

## Returns
`redirect` or `_redirect`: Returns a call to the `redirect` function for a single redirection or the `_redirect` function for multiple redirections.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

response = requests.get("https://api.example.com/redirect/3")

print(response.status_code)
print(response.history)
```
```javascript {% title="JavaScript" showLineNumbers=true %}
async function performRedirect() {
  const response = await fetch("https://api.example.com/redirect/4");
  const finalUrl = response.url;
  console.log(`Landed at: ${finalUrl}`);
  return finalUrl;
}

performRedirect();
```
```java {% title="Java" showLineNumbers=true %}
import java.net.HttpURLConnection;
import java.net.URL;

public class RedirectExample {
    public static void main(String[] args) throws Exception {
        URL url = new URL("https://api.example.com/redirect/5");
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("GET");
        connection.setInstanceFollowRedirects(false);

        int statusCode = connection.getResponseCode();
        String locationHeader = connection.getHeaderField("Location");
    }
}
```
```php {% title="PHP" showLineNumbers=true %}
<?php

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/redirect/5");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
curl_setopt($ch, CURLOPT_MAXREDIRS, 10);

$response = curl_exec($ch);

curl_close($ch);

echo $response;

?>
```
```go {% title="Go" showLineNumbers=true %}
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
	fmt.Printf("Location: %s\n", location)
}
```
```bash {% title="cURL" showLineNumbers=true %}
curl "https://api.example.com/redirect/3?absolute=true"
```
{% /codeGroup %}