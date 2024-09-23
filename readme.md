# nginx conf for ollama sorta

something to protect ollama api endpoints for such use cases lol using nginx for reverse proxy

- port 11343 must be close, as always. its basic common sense, you don't want anyone to spam your ai gpu server and whatnot.
- just change the port whenever, tho this is just an example.

## important part

self explanatory if you know what you are doing.

```nginx
map $http_authorization $auth_allowed {
  default 0; # Deny by default
  "my_ollama_secret_key" 1; # Allow only this specific api key
}
```

```nginx
location / {
  # Authorization check
  if ($auth_allowed = 0) {
    return 401; # Unauthorized if api key doesn't match
  }

  # ...
}
```

## some examples

### Get all models

```sh
curl http://localhost:6060/v1/models \
  -H "Authorization: my_ollama_secret_key"
```

### Example Request

```sh
curl http://localhost:6060/v1/chat/completions \
  -H "Authorization: my_ollama_secret_key" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "llama3.1",
    "messages": [
      { "role": "system", "content": "Always answer in rhymes." },
      { "role": "user", "content": "Introduce yourself." }
    ]
}'
```
