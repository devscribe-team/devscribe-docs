---
title: basic_auth
description: This API endpoint validates HTTP Basic Authentication credentials provided
  through the `user` and `passwd` path parameters. It checks the supplied credentials
  and, if they are valid, returns a JSON object confirming successful authentication
  along with the username. If the authentication fails, the endpoint responds with
  a 401 Unauthorized status code.
openapi: GET ['/basic-auth/<user>/<passwd>']
---
updated 3

## Summary
This API endpoint validates HTTP Basic Authentication credentials provided through the `user` and `passwd` path parameters. It checks the supplied credentials and, if they are valid, returns a JSON object confirming successful authentication along with the username. If the authentication fails, the endpoint responds with a 401 Unauthorized status code.

## API Info
{% cardGroup cols=2 %}
{% card title="HTTP Methods" icon="server" %}
`GET`
{% /card %}
{% card title="Route Path" icon="route" %}
`/basic-auth/<user>/<passwd>`
{% /card %}
{% /cardGroup %}

## Parameters
{% parameterField name="user" type="string" %}
The username for authentication; this is an optional parameter that defaults to "user".
{% /parameterField %}

{% parameterField name="passwd" type="string" %}
The password for authentication; this is an optional parameter that defaults to "passwd".
{% /parameterField %}

## Returns
`jsonify() or status_code()`: A function call that returns a `Response` object, containing a JSON payload on success or just an HTTP status code on failure.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

username = "testuser"
password = "testpassword"

url = f"https://api.example.com/basic-auth/{username}/{password}"

response = requests.get(url)

print(response.status_code)
print(response.json())
```
```javascript {% title="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/basic-auth/admin/secretpassword")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Error:", error));
```
```java {% title="Java" showLineNumbers=true %}
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class BasicAuthExample {
    public static void main(String[] args) throws Exception {
        String user = "test_user";
        String password = "a_secure_password";

        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/basic-auth/" + user + "/" + password))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println(response.body());
    }
}
```
```php {% title="PHP" showLineNumbers=true %}
<?php

$user = "testuser";
$passwd = "testpassword";

$url = "https://api.example.com/basic-auth/" . $user . "/" . $passwd;

$curl = curl_init($url);
curl_setopt($curl, CURLOPT_URL, $url);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($curl);
curl_close($curl);

echo $response;

?>
```
```go {% title="Go" showLineNumbers=true %}
package main

import (
	"fmt"
	"io"
	"log"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/basic-auth/testuser/testpass")
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
```bash {% title="cURL" showLineNumbers=true %}
curl "https://api.example.com/basic-auth/testuser/testpass"
```
{% /codeGroup %}

## Source
{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L949-L974)
{% /callout %}