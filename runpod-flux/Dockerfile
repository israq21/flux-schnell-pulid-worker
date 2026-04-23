FROM runpod/worker-comfyui:5.0.0-base

# --- Install PuLID-Flux custom nodes for face-locked character consistency ---
RUN cd /comfyui/custom_nodes && \
    git clone https://github.com/balazik/ComfyUI-PuLID-Flux.git && \
    cd ComfyUI-PuLID-Flux && \
    pip install --no-cache-dir -r requirements.txt

# --- Install PuLID dependencies ---
RUN pip install --no-cache-dir \
      insightface==0.7.3 \
      onnxruntime-gpu==1.20.1 \
      facexlib \
      timm \
      einops

# --- Point ComfyUI at the network volume for models ---
# The worker-comfyui image expects models at /comfyui/models/*.
# Our RunPod network volume is mounted at /runpod-volume and already contains
# ComfyUI/models/ populated with flux schnell + pulid + insightface files.
# Symlink so ComfyUI finds them.
RUN rm -rf /comfyui/models && \
    ln -s /runpod-volume/ComfyUI/models /comfyui/models

# Handler + entrypoint are inherited from the base image — nothing else needed.
