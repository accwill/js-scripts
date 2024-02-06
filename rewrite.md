# Rewrite Sample

Samples of HTTP rewrite feature.

## 修改 HTTP reqeust headers

- **Absolute URL of HTTP Request to match.**
``` text
https://example.com/resource4
```

- **Rewrite**
``` text
^https?://example\.com/resource4 url request-header (\r\n)User-Agent:.+(\r\n) request-header $1User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36$2
```

1. `^https?://example\.com/resource4`：这是一个正则表达式，表示匹配以 "http" 或 "https" 开头，后跟 "example.com/resource4" 的 URL。这是匹配的目标网址。
2. `url request-header (\r\n)User-Agent:.+(\r\n)`：这一部分是在匹配的目标 URL 上执行的操作。它将目标 URL 的请求头中的 "User-Agent" 一行找到，并在后面添加了一个换行符。这个部分的作用是修改请求头信息。
3. `request-header $1User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36$2`：这一部分是在第二步操作的基础上修改 "User-Agent" 的值。它将原始请求头中的 "User-Agent" 行替换为指定的用户代理信息。在这个例子中，用户代理信息被设置为模拟使用 macOS 10.11.1 版本的 Chrome 浏览器。

- **Before**

``` text
GET /resource4 HTTP/1.1
Host: example.com
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 12_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) CriOS/74.0.3729.155 Mobile/15E148 Safari/605.1
Accept-Language: en-us
Accept-Encoding: br, gzip, deflate
Connection: keep-alive
```

- **After**
``` text
GET /resource4 HTTP/1.1
Host: example.com
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36
Accept-Language: en-us
Accept-Encoding: br, gzip, deflate
Connection: keep-alive
```

## 修改 HTTP response body
The Content-Length will be automatically modified based on the body and encoding.

- **Absolute URL of HTTP Request to match.**
``` text
https://example.com/resource5
```

- **Rewrite**
``` text
^https?://example\.com/resource5 url response-body "info":\[.+\],"others" response-body "info":[],"others"
```

- **Before**
``` text
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
Cache-Control: no-cache, must-revalidate
Strict-Transport-Security: max-age=0
Connection: keep-alive
Content-Encoding: gzip
Content-Length: 64
```
``` text
{"basic":{"token":123},"info":[{"domain":"example.com"}],"others":"7sf43d59ccb7f5"}
```

- **After**
``` text
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
Cache-Control: no-cache, must-revalidate
Strict-Transport-Security: max-age=0
Connection: keep-alive
Content-Encoding: gzip
Content-Length: 48
```
``` text
{"basic":{"token":123},"info":[],"others":"7sf43d59ccb7f5"}
```

## 修改 HTTP response body using JavaScript
The Content-Length will be automatically modified based on the body and encoding.

- **Absolute URL of HTTP Request to match.**
``` text
https://example.com/resource5
```

- **Rewrite**
``` text
http://example\.com/resource5/ url script-response-body https://raw.githubusercontent.com/crossutility/Quantumult-X/master/sample-rewrite-with-script.js
```

- **Before**
``` text
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
Cache-Control: no-cache, must-revalidate
Strict-Transport-Security: max-age=0
Connection: keep-alive
Content-Encoding: gzip
Content-Length: 41
```
``` text
{"basic":{"token":123},"info":[{"domain":"example.com"}],"result":1}
```

- **After**
``` text
HTTP/1.1 200 OK
Content-Type: application/json; charset=UTF-8
Cache-Control: no-cache, must-revalidate
Strict-Transport-Security: max-age=0
Connection: keep-alive
Content-Encoding: gzip
Content-Length: 41
```
``` text
{"basic":{"token":123},"info":[{"domain":"example.com"}],"result":0}
```

