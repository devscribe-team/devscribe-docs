---
title: users_name
description: ''
api: GET /users/{user_id}
num: 1
---
## Summary
This API endpoint retrieves the name of a specific user based on the `user_id` provided in the URL path. It looks up the user in a static, in-memory data set and returns their name in a JSON response.

## Parameters
{% parameterField name="user_id" type="string" required=true %}
The unique identifier for the user.
{% /parameterField %}

## Returns
`jsonify`: Serializes the given arguments as JSON into a Response object.

## Usage Examples
{% codeGroup %}

```python {% filename="Python" showLineNumbers=true %}
import requests
import json

user_id = "1"
url = f"https://api.example.com/users/{user_id}"

try:
    response = requests.get(url)
    response.raise_for_status()
    user_name = response.json()
    print(f"Successfully retrieved user name: {user_name}")
except requests.exceptions.HTTPError as http_err:
    print(f"HTTP error occurred: {http_err}")
except Exception as err:
    print(f"An error occurred: {err}")
```

```javascript {% filename="JavaScript" showLineNumbers=true %}
fetch("https://api.example.com/users/1")
    .then(response => response.json())
    .then(userName => console.log(userName));
```

```java {% filename="Java" showLineNumbers=true %}
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class GetUserName {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.example.com/users/1"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println(response.body());
    }
}
```

```php {% filename="PHP" showLineNumbers=true %}
<?php

$userId = "1";
$url = "https://api.example.com/users/" . $userId;

$curl = curl_init($url);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($curl);
curl_close($curl);

echo $response;

?>
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
	resp, err := http.Get("https://api.example.com/users/1")
	if err != nil {
		log.Fatalf("Error making request: %s", err)
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Fatalf("Error reading response body: %s", err)
	}

	fmt.Println(string(body))
}

```

```bash {% filename="cURL" showLineNumbers=true %}
curl "https://api.example.com/users/1"
```
{% /codeGroup %}

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L240-L269)
{% /callout %}