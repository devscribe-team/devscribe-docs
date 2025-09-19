---
title: a
description: ''
api: GET /a
num: 1
---
## Summary
This function defines the `/a` API endpoint. It internally calls two other functions, `b` and `c`, with predefined integer values. The endpoint then returns a JSON object containing the results from both function calls, under the keys `b_result` and `c_result`.

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
`jsonify`: A Flask function that serializes a Python dictionary into a JSON formatted `Response` object.

## Usage Examples
{% codeGroup %}

```python {% filename="Python" showLineNumbers=true %}
import requests

response = requests.get("https://api.example.com/a")
print(response.json())
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
                .GET()
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println(response.statusCode());
        System.out.println(response.body());
    }
}
```

```php {% filename="PHP" showLineNumbers=true %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.example.com/a",
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

```go {% filename="GO" showLineNumbers=true %}
package main

import (
	"fmt"
	"io"
	"log"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/a")
	if err != nil {
		log.Fatal(err)
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Fatal(err)
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