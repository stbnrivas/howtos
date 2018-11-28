# Fake JSON Server

[github repo](https://github.com/typicode/json-server)
Get a full fake REST API with zero coding in less than 30 seconds (seriously)

```bash
npm install --global json-server
touch fake-backend.json
```

```json
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```



```bash
json-server --watch fake-backend.json
```

If you make POST, PUT, PATCH or DELETE requests, changes will be automatically and safely saved to JSON file

