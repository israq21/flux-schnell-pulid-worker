FROM runpod/worker-comfyui:5.0.0-base

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        python3-dev \
        python3.11-dev \
        python3.10-dev && \
    rm -rf /var/lib/apt/lists/*

RUN cd /comfyui/custom_nodes && \
    git clone https://github.com/balazik/ComfyUI-PuLID-Flux.git

RUN for PY in python3.10 python3.11; do \
        if command -v "$PY" >/dev/null 2>&1; then \
            echo "=== Installing for $PY ===" && \
            "$PY" -m pip install --no-cache-dir \
                insightface==0.7.3 \
                onnxruntime-gpu==1.20.1 \
                facexlib timm einops && \
            "$PY" -c "import insightface; print('$PY insightface OK', insightface.__version__)"; \
        fi; \
    done

RUN rm -rf /comfyui/models && \
    ln -s /runpod-volume/ComfyUI/models /comfyui/models

LABEL build.variant="pulid-flux-v5-dev-headers"
