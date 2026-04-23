FROM runpod/worker-comfyui:5.0.0-base

RUN set -eux && \
    cd /comfyui/custom_nodes && \
    git clone https://github.com/balazik/ComfyUI-PuLID-Flux.git && \
    cd ComfyUI-PuLID-Flux && \
    python3 -m pip install --no-cache-dir -r requirements.txt && \
    python3 -m pip install --no-cache-dir \
        insightface==0.7.3 \
        onnxruntime-gpu==1.20.1 \
        facexlib \
        timm \
        einops && \
    python3 -c "import insightface; print('insightface OK', insightface.__version__)" && \
    rm -rf /comfyui/models && \
    ln -s /runpod-volume/ComfyUI/models /comfyui/models

LABEL build.variant="pulid-flux-v3-py311"
