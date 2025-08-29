---
title: redirect_n_times
description: This endpoint initiates a chain of `n` HTTP 302 redirects, where `n`
  is an integer provided in the URL path. The final destination of the redirect chain
  is the `/get` endpoint. A query parameter, `absolute`, can be set to `true` to force
  the use of absolute URLs for each step of the redirect chain; otherwise, relative
  URLs are used by default.
openapi: GET ['/redirect/<int:n>']
---
# redirect_n_times

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L541-L567)
{% /callout %}

## Summary
This endpoint initiates a chain of `n` HTTP 302 redirects, where `n` is an integer provided in the URL path. The final destination of the redirect chain is the `/get` endpoint. A query parameter, `absolute`, can be set to `true` to force the use of absolute URLs for each step of the redirect chain; otherwise, relative URLs are used by default.

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
The number of times to redirect. This is a path parameter.
{% /parameterField %}

{% parameterField name="absolute" type="boolean" default="false" %}
An optional query parameter that specifies whether the redirect URLs should be absolute.
{% /parameterField %}

## Returns
Returns an HTTP 302 Redirect response to the next URL in the chain, or to `/get` for the final redirect.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

response = requests.get("https://api.example.com/redirect/3")

print(response.url)
print(response.status_code)
print(len(response.history))
```

```javascript {% title="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/redirect/5")
  .then(response => {
    console.log("Successfully redirected to:", response.url);
  })
  .catch(error => {
    console.error("Error during redirect:", error);
  });
```

```java {% title="Java" showLineNumbers=true %}
import java.net.HttpURLConnection;
import java.net.URL;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class RedirectExample {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://api.example.com/redirect/3");
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
            connection.setInstanceFollowRedirects(false);

            int responseCode = connection.getResponseCode();
            
            System.out.println("Response Code: " + responseCode);

            if (responseCode == HttpURLConnection.HTTP_MOVED_TEMP) {
                String location = connection.getHeaderField("Location");
                System.out.println("Redirected to: " + location);
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
	"io"
	"net/http"
)

func main() {
	client := &http.Client{}

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

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		fmt.Println(err)
		return
	}

	fmt.Println(string(body))
}
```

```bash {% title="cURL" showLineNumbers=true %}
curl -L "https://api.example.com/redirect/5?absolute=true"
```
{% /codeGroup %}