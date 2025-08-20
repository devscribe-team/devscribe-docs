---
title: set_cookie
description: This route handler sets a single cookie with a name and value specified
  in the URL path. Upon setting the cookie, it redirects the client to the main cookie-viewing
  endpoint to confirm the operation.
openapi: GET ['/cookies/set/<name>/<value>']
---
# set_cookie

**Source:** [Link](https://github.com/devscribe-team/httpbin/blob/complex/httpbin/core.py#L856-L879)

## Summary
{% callout type="info" %}
This route handler sets a single cookie with a name and value specified in the URL path. Upon setting the cookie, it redirects the client to the main cookie-viewing endpoint to confirm the operation.
{% /callout %}

## API Info
**HTTP Methods:** GET

**Route Path:** `/cookies/set/<name>/<value>`

## Usage Examples
{% codeGroup title="Usage Examples" %}
```python {% title="Python" %}
import requests

response = requests.get("https://api.example.com/cookies/set/user_id/12345")

print(response.status_code)
```

```javascript {% title="JavaScript" %}
fetch("https://api.example.com/cookies/set/token/qxw123")
  .then(response => response.text())
  .then(data => console.log(data));
```

```java {% title="Java" %}
import java.io.IOException;
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class SetCookieExample {
    public static void main(String[] args) {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/cookies/set/username/testuser"))
                .GET()
                .build();

        try {
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

$ch = curl_init("https://api.example.com/cookies/set/visit_id/1a2b3c4d5e");

curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HEADER, true);
curl_setopt($ch, CURLOPT_NOBODY, true);

$response = curl_exec($ch);

curl_close($ch);

var_dump($response);

?>
```

```go {% title="Go" %}
package main

import (
	"fmt"
	"net/http"
	"io"
)

func main() {
	resp, err := http.Get("https://api.example.com/cookies/set/session_id/abcdef123456")
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()

	fmt.Println("Response status:", resp.Status)
	body, err := io.ReadAll(resp.Body)
	if err != nil {
		panic(err)
	}
	fmt.Println(string(body))
}
```

```bash {% title="cURL" %}
curl -X GET "https://api.example.com/cookies/set/user/gemini"
```
{% /codeGroup %}

## Parameters
{% parameterField name="name" type="string" required=true %}
The name of the cookie to be set; this parameter is not optional.
{% /parameterField %}

{% parameterField name="value" type="string" required=true %}
The value to be assigned to the cookie; this parameter is not optional.
{% /parameterField %}

## Returns
{% callout type="info" %}
`redirect`: Returns a redirect response to the cookie list page.
{% /callout %}