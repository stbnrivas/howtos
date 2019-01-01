# curl: c url

to test need an API to tod

```bash
curl http://jsonplaceholder.typicode.com/posts
curl http://jsonplaceholder.typicode.com/posts/3
```

download file

```bash
curl --include $url
    # -i    --include   include protocol responde headers in output
curl --head $url
    # -I    --head      only show header
curl -output filename
    # -o    --output    write file instead of stdout
curl -O filename
    # -O   --remote-name   Write output to a file named as the remote file
```

# API test with Curl

## get request
default behaviour

```bash
curl $url
```

## post request

```bash
curl --data "title=Hello&body=Hello world" http://jsonplaceholder.typicode.com/posts
# you get response success
# {
#   "title": "hello",
#   "body": "hello-world",
#   "id": 101
# }
```


## put request

```bash
curl -X PUT -d "title=Hello" http://jsonplaceholder.typicode.com/posts/3
# {
#   "title": "Hello",
#   "id": 3
# }
curl http://jsonplaceholder.typicode.com/posts/3
```

## delete request

```bash
curl -X DELETE "http://jsonplaceholder.typicode.com/posts/3"
# {}
    # -X    --request <GET|POST|PUT|DELETE>
```


# authentication with curl using ftp credentials

```bash
curl -u user:secret $url
```
using ftp credentials

```bash
# upload
curl -u user:secret -T $fiename ftp://ftp.domain.com
# download
curl -u user:secret -O $fiename ftp://ftp.domain.com/filename
```

# follow 301 redirection

```bash
curl http://google.com
# <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
# <TITLE>301 Moved</TITLE></HEAD><BODY>
# <H1>301 Moved</H1>
# The document has moved
# <A HREF="http://www.google.com/">here</A>.
# </BODY></HTML>
curl -L http://google.com
```
