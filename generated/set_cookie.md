---
title: set_cookie
description: This endpoint sets a cookie using a name and value provided in the URL
  path. After the cookie is successfully set on the response, the client is redirected
  to the endpoint for viewing all cookies. The cookie's `secure` flag is set based
  on the request's scheme.
openapi: GET ['/cookies/set/<name>/<value>']
---
## Summary
This endpoint sets a cookie using a name and value provided in the URL path. After the cookie is successfully set on the response, the client is redirected to the endpoint for viewing all cookies. The cookie's `secure` flag is set based on the request's scheme.

## Parameters
{% parameterField name="name" type="string" required=true %}
The name of the cookie to set.
{% /parameterField %}

{% parameterField name="value" type="string" required=true %}
The value to assign to the cookie.
{% /parameterField %}

## Returns
`werkzeug.wrappers.response.Response`: A Response object that sets a cookie and then redirects the client to the cookie list page.

## Usage Examples
{% codeGroup %}

```python {% filename="Python" showLineNumbers=true %}
import requests

url = "https://api.example.com/cookies/set/user_token/a1b2c3d4e5"
response = requests.get(url, allow_redirects=True)

print(f"Status Code: {response.status_code}")
print("Cookies after redirect:")
for cookie, value in response.cookies.items():
    print(f"{cookie}: {value}")
```

```javascript {% filename="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/cookies/set/user/gemini")
  .then(response => {
    if (response.ok) {
      console.log("Cookie set successfully.");
    } else {
      console.error("Failed to set cookie.");
    }
  })
  .catch(error => console.error("Error:", error));
```

```java {% filename="Java" showLineNumbers=true %}
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class SetCookieExample {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newBuilder()
                .followRedirects(HttpClient.Redirect.NEVER)
                .build();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/cookies/set/session-id/abc123xyz"))
                .build();

        HttpResponse<Void> response = client.send(request, HttpResponse.BodyHandlers.discarding());

        System.out.println("Status Code: " + response.statusCode());
        response.headers().firstValue("Set-Cookie").ifPresent(header -> System.out.println("Set-Cookie: " + header));
    }
}

```

```php {% filename="PHP" showLineNumbers=true %}
<?php

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/cookies/set/session_id/abc123xyz");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
curl_setopt($ch, CURLOPT_COOKIEJAR, "cookies.txt");
curl_setopt($ch, CURLOPT_COOKIEFILE, "cookies.txt");

$response = curl_exec($ch);

curl_close($ch);

echo $response;

?>
```

```go {% filename="GO" showLineNumbers=true %}
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

	req, err := http.NewRequest("GET", "https://api.example.com/cookies/set/user/gemini", nil)
	if err != nil {
		fmt.Println("Error creating request:", err)
		return
	}

	resp, err := client.Do(req)
	if err != nil {
		fmt.Println("Error sending request:", err)
		return
	}
	defer resp.Body.Close()

	fmt.Println("Status Code:", resp.StatusCode)
	for _, cookie := range resp.Cookies() {
		fmt.Printf("Cookie: %s=%s\n", cookie.Name, cookie.Value)
	}
}

```

```bash {% filename="cURL" showLineNumbers=true %}
curl "https://api.example.com/cookies/set/session_token/a1b2c3d4e5f6"
```
{% /codeGroup %}

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L877-L900)
{% /callout %}