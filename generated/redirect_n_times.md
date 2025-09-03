---
title: redirect_n_times
description: This API endpoint initiates a chain of `n` HTTP 302 redirects, where
  `n` is an integer specified in the URL path. The final destination of the redirect
  chain is the `/get` endpoint. By default, the redirects use relative URLs. To use
  absolute URLs, an optional `absolute` query parameter can be set to `true`.
openapi: GET ['/redirect/<int:n>']
---
# redirect_n_times

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L541-L567)
{% /callout %}

## Summary
This API endpoint initiates a chain of `n` HTTP 302 redirects, where `n` is an integer specified in the URL path. The final destination of the redirect chain is the `/get` endpoint. By default, the redirects use relative URLs. To use absolute URLs, an optional `absolute` query parameter can be set to `true`.

## API Info
{% cardGroup cols=2 gap="sm" %}
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
An optional query parameter that determines if the redirect is absolute.
{% /parameterField %}

## Returns
`redirect` or `_redirect`: Returns a function call to either `redirect` or `_redirect`, both of which generate a 302 redirect response.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

url = "https://api.example.com/redirect/5"
params = {"absolute": "true"}
response = requests.get(url, params=params)

print(response.status_code)
print(response.url)
```
```javascript {% title="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/redirect/5?absolute=true")
  .then(response => response.text())
  .then(data => console.log(data))
  .catch(error => console.error("Error:", error));
```
```java {% title="Java" showLineNumbers=true %}
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class RedirectExample {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://api.example.com/redirect/5");
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
            connection.setInstanceFollowRedirects(false);

            int status = connection.getResponseCode();

            if (status == HttpURLConnection.HTTP_MOVED_TEMP) {
                String newUrl = connection.getHeaderField("Location");
                System.out.println("Redirected to URL: " + newUrl);
            }

            connection.disconnect();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
```php {% title="PHP" showLineNumbers=true %}
<?php

$ch = curl_init();

curl_setopt_array($ch, [
    CURLOPT_URL => "https://api.example.com/redirect/5",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_MAXREDIRS => 5,
]);

$response = curl_exec($ch);

curl_close($ch);

echo $response;

?>
```
```go {% title="GO" showLineNumbers=true %}
package main

import (
	"fmt"
	"io"
	"net/http"
)

func main() {
	client := &http.Client{}

	req, err := http.NewRequest("GET", "https://api.example.com/redirect/5", nil)
	if err != nil {
		fmt.Println("Error creating request:", err)
		return
	}

	resp, err := client.Do(req)
	if err != nil {
		fmt.Println("Error making request:", err)
		return
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		fmt.Println("Error reading response body:", err)
		return
	}

	fmt.Printf("Status Code: %d\n", resp.StatusCode)
	fmt.Printf("Response Body: %s\n", string(body))
}
```
```bash {% title="cURL" showLineNumbers=true %}
curl "https://api.example.com/redirect/3?absolute=true"
```
{% /codeGroup %}