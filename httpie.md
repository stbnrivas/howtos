# httpie

```
sudo apt install httpie
```

## usage

```
http [flags] [METHOD] URL [ITEM [ITEM]]
```


```
http -v httpbin.org/get

	GET /get HTTP/1.1
	Accept: */*
	Accept-Encoding: gzip, deflate
	Connection: keep-alive
	Host: httpbin.org
	User-Agent: HTTPie/0.9.8



	HTTP/1.1 200 OK
	Access-Control-Allow-Credentials: true
	Access-Control-Allow-Origin: *
	Connection: keep-alive
	Content-Length: 297
	Content-Type: application/json
	Date: Sun, 31 Jan 2021 18:22:40 GMT
	Server: gunicorn/19.9.0

	{
	    "args": {},
	    "headers": {
	        "Accept": "*/*",
	        "Accept-Encoding": "gzip, deflate",
	        "Host": "httpbin.org",
	        "User-Agent": "HTTPie/0.9.8",
	        "X-Amzn-Trace-Id": "Root=1-6016f570-1fac325726c7ec210d984aaa"
	    },
	    "origin": "188.78.219.215",
	    "url": "http://httpbin.org/get"
	}
```


## usage with headers


```
http $(URL)  User-Agent:Bacon/1.0  'Cookie:valued-visitor=yes;foo=bar' X-Foo:Bar  Referer:https://httpie.org/
```


```
http $(URL)  User-Agent:Bacon/1.0  'Cookie:valued-visitor=yes;foo=bar' X-Foo:Bar  Referer:https://httpie.org/
```


## usage with params

```
http $(URL) foo==bar wicked==witch
```


## usage with verbs

```
http POST $(URL) wicked=witch casts:='["spells", "curses"]' --json
```



## usage authentication


```
http -a username:password pie.dev/basic-auth/username/password
http -a username:         pie.dev/headers


http -A digest -a username:password pie.dev/digest-auth/httpie/username/password

```