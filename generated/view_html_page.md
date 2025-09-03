---
title: view_html_page
description: This function defines the `/html` endpoint, which responds to GET requests
  by rendering and returning the `moby.html` template as a simple HTML document. For
  debugging purposes, it also prints the incoming request headers to the server's
  console.
openapi: GET ['/html']
---
# view_html_page

{% callout type="tip" %}
View source on [**GitHub ↗**](https://github.com/devscribe-team/httpbin/blob/master/httpbin/core.py#L246-L263)
{% /callout %}

## Summary
This function defines the `/html` endpoint, which responds to GET requests by rendering and returning the `moby.html` template as a simple HTML document. For debugging purposes, it also prints the incoming request headers to the server's console.

## API Info
{% cardGroup cols=2 %}
  {% card title="HTTP Methods" icon="server" description="" %}
  `GET`
  {% /card %}
  {% card title="Route Path" icon="route" description="" %}
  `/html`
  {% /card %}
{% /cardGroup %}

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
`render_template()`: A function that renders a template into an HTML string.

## Usage Examples
{% codeGroup %}
```python {% title="Python" showLineNumbers=true %}
import requests

response = requests.get("https://api.example.com/html")

print(response.text)
```

```javascript {% title="JavaScript" showLineNumbers=true %}
async function getHtml() {
  const response = await fetch("https://api.example.com/html");
  const html = await response.text();
  console.log(html);
}

getHtml();
```

```java {% title="Java" showLineNumbers=true %}
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Example {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://api.example.com/html");
            HttpURLConnection con = (HttpURLConnection) url.openConnection();
            con.setRequestMethod("GET");

            int status = con.getResponseCode();
            System.out.println("Response Code: " + status);

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
            String inputLine;
            StringBuffer content = new StringBuffer();
            while ((inputLine = in.readLine()) != null) {
                content.append(inputLine);
            }
            in.close();
            con.disconnect();

            System.out.println("Response Body: " + content.toString());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

```php {% title="PHP" showLineNumbers=true %}
<?php

$ch = curl_init("https://api.example.com/html");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);
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
	resp, err := http.Get("https://api.example.com/html")
	if err != nil {
		log.Fatalf("Error fetching URL: %v", err)
	}
	defer resp.Body.Close()

	if resp.StatusCode != http.StatusOK {
		log.Fatalf("Error: received status code %d", resp.StatusCode)
	}

	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Fatalf("Error reading response body: %v", err)
	}

	fmt.Println(string(body))
}
```

```bash {% title="cURL" showLineNumbers=true %}
curl -X GET "https://api.example.com/html"
```
{% /codeGroup %}