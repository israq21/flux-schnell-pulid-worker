# Flux Schnell + PuLID Custom Worker

Custom RunPod serverless worker for Flux.1-schnell with PuLID-Flux face consistency.

## Deployment

1. Put `Dockerfile` in a new GitHub repo (public or private).
2. On RunPod → Serverless → New Endpoint → select "GitHub Repo" → paste your repo URL.
3. RunPod auto-builds the image.
4. Attach network volume `flux-models` at `/runpod-volume`.
5. GPU: RTX 4090, Max Workers: 5, Flashboot: on, Idle timeout: 5s.

## Inputs (same as runpod-workers/worker-comfyui)

```json
{
  "input": {
    "workflow": { ... },
    "images": [{ "name": "ref.jpg", "image": "<base64>" }]
  }
}
```

Used by `shared/runpod-with-refs.mjs`.
