---
title: view_headers
description: This API endpoint, available at `/headers`, is designed for request inspection.
  It captures the complete set of HTTP headers from an incoming request and returns
  them as a JSON object.
openapi: GET ['/headers']
---
# view_headers

**Source:** [Link](https://github.com/devscribe-team/httpbin/blob/complex/httpbin/core.py#L332-L345)

{% callout type="info" %}
This API endpoint, available at `/headers`, is designed for request inspection. It captures the complete set of HTTP headers from an incoming request and returns them as a JSON object.
{% /callout %}

## API Info

{% cardGroup cols=2 %}
  {% card title="HTTP Method" %}
    `GET`
  {% /card %}
  {% card title="Route Path" %}
    `/headers`
  {% /card %}
{% /cardGroup %}

## Usage Examples
{% codeGroup %}
```python {% title="Python" %}
import requests

url = "https://api.example.com/headers"
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3",
    "Accept": "application/json",
    "Accept-Language": "en-US,en;q=0.5",
    "X-Custom-Header": "MyCustomValue"
}

response = requests.get(url, headers=headers)

print(response.json())
```

```javascript {% title="JavaScript" %}
fetch("https://api.example.com/headers", {
  headers: {
    "X-Custom-Header": "MyValue",
    "User-Agent": "MyClient/1.0"
  }
})
.then(response => response.json())
.then(data => console.log(data));
```

```java {% title="Java" %}
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Example {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://api.example.com/headers");
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");
            conn.setRequestProperty("Accept", "application/json");
            conn.setRequestProperty("X-Custom-Header", "value123");

            if (conn.getResponseCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : " + conn.getResponseCode());
            }

            BufferedReader br = new BufferedReader(new InputStreamReader((conn.getInputStream())));
            String output;
            System.out.println("Output from Server .... \n");
            while ((output = br.readLine()) != null) {
                System.out.println(output);
            }
            conn.disconnect();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

```php {% title="PHP" %}
$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.example.com/headers",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => [
    "X-Custom-Header: my-custom-value",
    "User-Agent: My-PHP-Client/1.0",
    "Accept: application/json"
  ],
]);

$response = curl_exec($curl);

curl_close($curl);

echo $response;
```

```go {% title="GO" %}
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func main() {
	client := &http.Client{}
	req, err := http.NewRequest("GET", "https://api.example.com/headers", nil)
	if err != nil {
		fmt.Println(err)
		return
	}
	req.Header.Set("User-Agent", "Go-http-client/1.1")
	req.Header.Set("X-Custom-Header", "my-custom-value")
	resp, err := client.Do(req)
	if err != nil {
		fmt.Println(err)
		return
	}
	defer resp.Body.Close()
	body, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		fmt.Println(err)
		return
	}
	fmt.Println(string(body))
}
```

```bash {% title="cURL" %}
curl "https://api.example.com/headers" -H "X-Request-ID: abc-123" -H "User-Agent: MyClient/1.0"
```
{% /codeGroup %}

## Parameters
{% callout type="info" %}
No parameters.
{% /callout %}

## Returns
{% parameterField name="jsonify" type="Flask Response Object" %}
A function that serializes a Python dictionary into a JSON formatted string and wraps it in a Flask `Response` object.
{% /parameterField %}