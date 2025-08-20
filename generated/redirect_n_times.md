---
title: redirect_n_times
description: This endpoint initiates a chain of 302 redirects, with the total number
  of hops specified by the integer `n` in the URL path. Our implementation supports
  both relative and absolute redirects, which can be controlled via the optional `absolute`
  query parameter. The final redirect in the sequence always terminates at the `/get`
  endpoint, completing the chain.
openapi: GET ['/redirect/<int:n>']
---
# redirect_n_times

{% card title="View Source Code" description="httpbin/core.py#L537-L563" icon="github" href="https://github.com/devscribe-team/httpbin/blob/complex/httpbin/core.py#L537-L563" /%}

## Summary
This endpoint initiates a chain of 302 redirects, with the total number of hops specified by the integer `n` in the URL path. Our implementation supports both relative and absolute redirects, which can be controlled via the optional `absolute` query parameter. The final redirect in the sequence always terminates at the `/get` endpoint, completing the chain.

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Method" icon="server" %}
`GET`
{% /card %}
{% card title="Route Path" icon="link" %}
`/redirect/<int:n>`
{% /card %}
{% /cardGroup %}

## Usage Examples
{% codeGroup title="Usage Examples" %}
```python {% title="Python" %}
import requests

response = requests.get("https://api.example.com/redirect/3")

print(response.history)
print(response.status_code)
```

```javascript {% title="JavaScript" %}
fetch("https://api.example.com/redirect/6")
  .then(response => response.text())
  .then(html => console.log(html))
  .catch(error => console.error("Error:", error));
```

```java {% title="Java" %}
import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.URL;

public class Main {
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
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```php {% title="PHP" %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
    CURLOPT_URL => "https://api.example.com/redirect/3",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_MAXREDIRS => 10,
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
	"os"
)

func main() {
	client := &http.Client{}

	req, err := http.NewRequest("GET", "https://api.example.com/redirect/5", nil)
	if err != nil {
		fmt.Fprintf(os.Stderr, "Error creating request: %v\n", err)
		os.Exit(1)
	}

	resp, err := client.Do(req)
	if err != nil {
		fmt.Fprintf(os.Stderr, "Error making request: %v\n", err)
		os.Exit(1)
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		fmt.Fprintf(os.Stderr, "Error reading response body: %v\n", err)
		os.Exit(1)
	}

	fmt.Println(string(body))
}
```

```bash {% title="cURL" %}
curl "https://api.example.com/redirect/5"
```
{% /codeGroup %}

## Parameters
{% parameterField name="n" type="integer" required=true %}
A path parameter that specifies the number of times to redirect.
{% /parameterField %}

{% parameterField name="absolute" type="boolean" default="false" %}
A query parameter that determines if the redirect is absolute.
{% /parameterField %}

## Returns
{% callout type="info" %}
A `302 Found` redirect response to the next URL in the chain, ultimately terminating at the `/get` endpoint.
{% /callout %}