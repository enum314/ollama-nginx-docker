## Get all models

```sh
curl http://localhost:6060/v1/models \
  -H "Authorization: my_ollama_secret_key"
```

## Example Request

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
