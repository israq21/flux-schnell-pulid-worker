FROM runpod/worker-comfyui:5.0.0-base

RUN set -eux && \
    cd /comfyui/custom_nodes && \
    git clone https://github.com/balazik/ComfyUI-PuLID-Flux.git && \
    for PY in python3.10 python3.11 python3; do \
        if command -v "$PY" >/dev/null 2>&1; then \
            echo "=== Installing for $PY ===" && \
            "$PY" -m pip install --no-cache-dir -r /comfyui/custom_nodes/ComfyUI-PuLID-Flux/requirements.txt && \
            "$PY" -m pip install --no-cache-dir \
                insightface==0.7.3 \
                onnxruntime-gpu==1.20.1 \
                facexlib \
                timm \
                einops && \
            "$PY" -c "import insightface; print('$PY insightface OK', insightface.__version__)"; \
        fi; \
    done && \
    rm -rf /comfyui/models && \
    ln -s /runpod-volume/ComfyUI/models /comfyui/models

LABEL build.variant="pulid-flux-v4-multi-py"
