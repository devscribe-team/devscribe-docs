---
title: a
description: This API endpoint, accessible at the `/a` path, calls two internal functions,
  `b` and `c`, with fixed integer arguments. It then returns a JSON object containing
  the results from both function calls, keyed as `c_result` and `b_result` respectively.
openapi: GET ['/a']
---
## Summary
This API endpoint, accessible at the `/a` path, calls two internal functions, `b` and `c`, with fixed integer arguments. It then returns a JSON object containing the results from both function calls, keyed as `c_result` and `b_result` respectively.

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
`jsonify`: Serializes the provided dictionary into a JSON-formatted `Response` object.

## Usage Examples
{% codeGroup %}

```python {% filename="Python" showLineNumbers=true %}
import requests

response = requests.get("https://api.example.com/a")
data = response.json()

print(data)
```

```javascript {% filename="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/a")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Error:", error));
```

```java {% filename="Java" showLineNumbers=true %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Example {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/a"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println(response.body());
    }
}
```

```php {% filename="PHP" showLineNumbers=true %}
<?php
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/a");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

$response = curl_exec($ch);

if(curl_errno($ch)){
    echo "Error:" . curl_error($ch);
}

curl_close($ch);

$data = json_decode($response, true);
print_r($data);
?>
```

```go {% filename="GO" showLineNumbers=true %}
package main

import (
	"fmt"
	"io"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/a")
	if err != nil {
		fmt.Println("Error making request:", err)
		return
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		fmt.Println("Error reading response:", err)
		return
	}

	fmt.Println(string(body))
}

```

```bash {% filename="cURL" showLineNumbers=true %}
curl "https://api.example.com/a"
```
{% /codeGroup %}

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L240-L247)
{% /callout %}