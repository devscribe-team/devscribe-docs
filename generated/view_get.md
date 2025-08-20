---
title: view_get
description: This function powers our `/get` endpoint, which is designed to handle
  HTTP GET requests. It returns a JSON object that reflects the incoming request's
  details, specifically its query string arguments, headers, URL, and the client's
  origin IP address.
openapi: GET ['/get']
---
# view_get

**Source:** [Link](https://github.com/devscribe-team/httpbin/blob/complex/httpbin/core.py#L366-L379)

## Summary

{% callout type="info" %}
This function powers our `/get` endpoint, which is designed to handle HTTP GET requests. It returns a JSON object that reflects the incoming request's details, specifically its query string arguments, headers, URL, and the client's origin IP address.
{% /callout %}

## API Info

{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
GET
{% /card %}
{% card title="Route Path" icon="link" %}
/get
{% /card %}
{% /cardGroup %}

## Usage Examples

{% codeGroup %}
```python {% title="Python" %}
import requests

url = "https://api.example.com/get"
params = {"show_env": "1"}
headers = {"X-Request-ID": "a-unique-request-id"}

response = requests.get(url, params=params, headers=headers)

print(response.json())
```

```javascript {% title="JavaScript" %}
fetch("https://api.example.com/get?name=JohnDoe&age=30")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Error:", error));
```

```java {% title="Java" %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class SimpleGetRequest {
    public static void main(String[] args) {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/get?show_env=1"))
                .build();

        try {
            HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
            System.out.println(response.body());
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

```php {% title="PHP" %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.example.com/get?param1=value1&param2=value2",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => [
    "X-My-Header: 12345"
  ],
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

```go {% title="Go" %}
package main

import (
	"fmt"
	"io"
	"net/http"
)

func main() {
	client := &http.Client{}
	req, err := http.NewRequest("GET", "https://api.example.com/get?show_env=1", nil)
	if err != nil {
		fmt.Println(err)
		return
	}
	req.Header.Add("X-Request-Id", "f6f0481a-2263-4328-973c-22a43de4afb3")
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

```bash {% title="cURL" %}
curl -X GET "https://api.example.com/get?param1=value1&param2=value2"
```
{% /codeGroup %}

## Parameters

{% callout type="info" %}
This endpoint does not accept any parameters.
{% /callout %}

## Returns

{% parameterField name="Response Body" type="JSON Object" required=true %}
The endpoint returns a JSON object that reflects the incoming request's details, including its query string arguments, headers, URL, and the client's origin IP address.
{% /parameterField %}