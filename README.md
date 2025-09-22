# Self Chat Phone

A single-page phone-style chat that lets two virtual contacts carry on an autonomous text conversation using any local Ollama model. Pick a model from the dropdown and watch Alex and Blair volley short, natural replies forever.

## Prerequisites
- [Ollama](https://ollama.com) running locally (`ollama serve`).
- CORS access from the browser to Ollama. If your browser blocks requests, launch Ollama with `OLLAMA_ORIGINS=*` (for example: `OLLAMA_ORIGINS=* ollama serve`).

## Run It
1. Open this project in Pinokio.
2. Launch the app (Pinokio will serve `index.html`).
3. Select a model from the dropdown and let the chat flow. Switching models resets the conversation with the new model instantly.

The interface mimics a modern phone SMS app, complete with a live status indicator and an iPhone-inspired tri-tone chime (tap/click once to unlock audio). Alex and Blair keep their replies to short, readable bursts so you can follow along in real time.

## API Cheatsheet
Use these endpoints on your local Ollama instance (`http://localhost:11434`).

### JavaScript
```js
const base = "http://localhost:11434";
const models = await fetch(`${base}/api/tags`).then((r) => r.json());

const reply = await fetch(`${base}/api/generate`, {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({
    model: "llama3",
    prompt: "Write a single friendly chat reply.",
    stream: false
  })
}).then((r) => r.json());
```

### Python
```python
import requests

base = "http://localhost:11434"
models = requests.get(f"{base}/api/tags").json()

payload = {
    "model": "llama3",
    "prompt": "Write a single friendly chat reply.",
    "stream": False,
}
reply = requests.post(f"{base}/api/generate", json=payload).json()
```

### curl
```bash
curl http://localhost:11434/api/generate \
  -H 'Content-Type: application/json' \
  -d '{
    "model": "llama3",
    "prompt": "Write a single friendly chat reply.",
    "stream": false
  }'
```

## Notes
- Refresh the page if you want to clear the conversation manually.
- If you see connection errors, confirm Ollama is running and accessible at `http://localhost:11434` with permissive CORS settings.
- If Ollama is offline you'll see an in-app red banner reminding you to start `ollama serve`.
