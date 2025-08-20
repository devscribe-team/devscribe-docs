---
title: view_origin
description: This API endpoint returns the origin IP address of an incoming request
  as a JSON object. To ensure accuracy when our service operates behind a proxy or
  load balancer, it prioritizes the `X-Forwarded-For` header to identify the client.
  If this header is unavailable, the endpoint defaults to the request's immediate
  remote address.
openapi: GET ['/ip']
---
# view_origin

**Source:** [Link](https://github.com/devscribe-team/httpbin/blob/complex/httpbin/core.py#L300-L313)

## Summary
{% callout type="info" %}
This API endpoint returns the origin IP address of an incoming request as a JSON object. To ensure accuracy when our service operates behind a proxy or load balancer, it prioritizes the `X-Forwarded-For` header to identify the client. If this header is unavailable, the endpoint defaults to the request's immediate remote address.
{% /callout %}

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Method" icon="server" %}
`GET`
{% /card %}
{% card title="Route Path" icon="link" %}
`/ip`
{% /card %}
{% /cardGroup %}

## Usage Examples
{% codeGroup title="API Request Examples" %}
```python {% filename="example.py" %}
import requests
import json

def get_my_ip():
    url = "https://api.example.com/ip"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        print(f"My IP address is: {data.get('origin')}")
    else:
        print(f"Failed to retrieve IP address. Status code: {response.status_code}")

get_my_ip()
```

```javascript {% filename="example.js" %}
fetch("https://api.example.com/ip")
  .then(response => response.json())
  .then(data => console.log(data.origin))
  .catch(error => console.error("Error:", error));
```

```java {% filename="Main.java" %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/ip"))
                .build();

        HttpResponse<String> response = client.send(request,
                HttpResponse.BodyHandlers.ofString());

        System.out.println(response.body());
    }
}
```

```php {% filename="example.php" %}
<?php

$curl = curl_init();

curl_setopt_array($curl, [
    CURLOPT_URL => "https://api.example.com/ip",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CUSTOMREQUEST => "GET",
]);

$response = curl_exec($curl);

curl_close($curl);

echo $response;

```

```go {% filename="main.go" %}
package main

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
	"net/http"
)

type IPResponse struct {
	Origin string `json:"origin"`
}

func main() {
	resp, err := http.Get("https://api.example.com/ip")
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()

	body, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		panic(err)
	}

	var ipResponse IPResponse
	err = json.Unmarshal(body, &ipResponse)
	if err != nil {
		panic(err)
	}

	fmt.Printf("Origin IP: %s\n", ipResponse.Origin)
}

```

```bash {% title="cURL" %}
curl "https://api.example.com/ip"
```
{% /codeGroup %}

## Parameters
{% callout type="info" %}
This endpoint does not accept any parameters.
{% /callout %}

## Returns
Returns a JSON object containing the origin IP address of the request.

{% parameterField name="origin" type="string" required=true %}
The origin IP address of the request.
{% /parameterField %}

### Example Response
```json
{
  "origin": "123.45.67.89"
}
```