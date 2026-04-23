FROM runpod/worker-comfyui:5.0.0-base

RUN cd /comfyui/custom_nodes && \
    git clone https://github.com/balazik/ComfyUI-PuLID-Flux.git

RUN python3.11 -m pip install --no-cache-dir \
      insightface==0.7.3 \
      onnxruntime-gpu==1.20.1 \
      facexlib timm einops || \
    python3.10 -m pip install --no-cache-dir \
      insightface==0.7.3 \
      onnxruntime-gpu==1.20.1 \
      facexlib timm einops

RUN rm -rf /comfyui/models && \
    ln -s /runpod-volume/ComfyUI/models /comfyui/models
