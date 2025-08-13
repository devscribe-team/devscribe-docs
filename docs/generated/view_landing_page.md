---
title: view_landing_page
description: ''
openapi: ' '
---
# view_landing_page

**Source:** [Link](https://github.com/devscribe-team/httpbin/blob//httpbin/core.py#L240-L243)

## Summary


## API Info
None

## Usage Example
### Python
```python
import requests

response = requests.get("http://127.0.0.1:5000/legacy")
print(response.status_code)

```

### JavaScript
```javascript

fetch("https://api.example.com/legacy", {
  method: "GET"
})
.then(response => response.text())
.then(html => {
  console.log(html);
})
.catch(error => {
  console.error("Error:", error);
});

```

### Java
```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://httpbin.org/legacy"))
    .build();
try {
    HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
    System.out.println(response.body());
} catch (IOException | InterruptedException e) {
    e.printStackTrace();
}
```

### PHP
```php
<?php
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/legacy");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);

curl_close($ch);

echo $response;
?>
```

### GO
```go
package main

import (
	"fmt"
	"io"
	"log"
	"net/http"
)

func main() {
	resp, err := http.Get("https://api.example.com/legacy")
	if err != nil {
		log.Fatalf("error making request: %s", err)
	}
	defer resp.Body.Close()

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Fatalf("error reading response body: %s", err)
	}

	fmt.Println(string(body))
}

```

### cURL
```bash
curl "https://api.example.com/legacy"
```

## Parameters
No parameters.

## Returns
`render_template()`: This function renders a template from the template folder with the given context.
