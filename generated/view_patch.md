---
title: view_patch
description: "This endpoint is bound to the `/patch` route and specifically handles\
  \ `PATCH` requests. Its primary function is to serve as a testing utility by reflecting\
  \ the incoming request's data back to the client. It aggregates various components\
  \ of the request\u2014including the URL, query arguments, form data, raw data body,\
  \ headers, any multipart files, and the JSON payload\u2014into a single JSON response."
openapi: PATCH ['/patch']
---
# view_patch

**Source:** [Link](https://github.com/devscribe-team/httpbin/blob/complex/httpbin/core.py#L450-L465)

## Summary

{% callout type="info" %}
This endpoint is bound to the `/patch` route and specifically handles `PATCH` requests. Its primary function is to serve as a testing utility by reflecting the incoming request's data back to the client. It aggregates various components of the request—including the URL, query arguments, form data, raw data body, headers, any multipart files, and the JSON payload—into a single JSON response.
{% /callout %}

## API Info

{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
`PATCH`
{% /card %}
{% card title="Route Path" icon="link" %}
`/patch`
{% /card %}
{% /cardGroup %}

## Usage Example

{% codeGroup %}

```python {% title="Python" %}
import requests

url = "https://api.example.com/patch"
payload = {"name": "Jane Doe", "email": "jane.doe@example.com"}

response = requests.patch(url, json=payload)

print(response.json())
```

```javascript {% title="JavaScript" %}
fetch("https://api.example.com/patch", {
  method: "PATCH",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    "email": "new.email@example.com"
  })
})
.then(response => response.json())
.then(data => console.log(data));
```

```java {% title="Java" %}
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.io.IOException;

public class ApiExample {
    public static void main(String[] args) {
        try {
            HttpClient client = HttpClient.newHttpClient();
            String requestBody = "{\"name\": \"John Doe\", \"status\": \"active\"}";

            HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/patch"))
                .method("PATCH", HttpRequest.BodyPublishers.ofString(requestBody))
                .header("Content-Type", "application/json")
                .build();

            HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

            System.out.println("Status Code: " + response.statusCode());
            System.out.println("Response Body: " + response.body());
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
  CURLOPT_URL => "https://api.example.com/patch",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "PATCH",
  CURLOPT_POSTFIELDS => "{\n    \"key\": \"value\"\n}",
  CURLOPT_HTTPHEADER => [
    "Content-Type: application/json"
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
	"bytes"
	"fmt"
	"io"
	"net/http"
)

func main() {
	url := "https://api.example.com/patch"
	payload := []byte(`{"name": "John Doe", "email": "john.doe@example.com"}`)

	req, err := http.NewRequest("PATCH", url, bytes.NewBuffer(payload))
	if err != nil {
		panic(err)
	}
	req.Header.Set("Content-Type", "application/json")

	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		panic(err)
	}
	fmt.Println(string(body))
}
```

```bash {% title="cURL" %}
curl -X PATCH "https://api.example.com/patch" -H "Content-Type: application/json" -d "{\"key\":\"value\"}"
```

{% /codeGroup %}

## Parameters

{% parameterField name="args" type="dict" %}
The query string arguments from the request URL.
{% /parameterField %}

{% parameterField name="data" type="str" %}
The raw request body, returned as a string.
{% /parameterField %}

{% parameterField name="files" type="dict" %}
A dictionary of files uploaded via a multipart form.
{% /parameterField %}

{% parameterField name="form" type="dict" %}
A dictionary of form data from the request.
{% /parameterField %}

{% parameterField name="json" type="dict" %}
The JSON payload from the request, if the `Content-Type` is `application/json`.
{% /parameterField %}

## Returns

{% card title="JSON Response" icon="package" %}
Returns a JSON object that reflects all the data sent in the request. This includes headers, query arguments, form data, files, and the JSON payload.
{% /card %}