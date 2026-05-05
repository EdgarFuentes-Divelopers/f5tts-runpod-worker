FROM ghcr.io/swivid/f5-tts:main

# Guardar versión exacta de torch antes de que pip toque algo
RUN python -c "import torch; v=torch.__version__; open('/torch_ver.txt','w').write(v)"

# Instalar runpod completo, luego restaurar torch/torchaudio a la versión original
RUN pip install --no-cache-dir runpod && \
    TORCH_VER=$(cat /torch_ver.txt) && \
    pip install --no-cache-dir \
        "torch==${TORCH_VER}" \
        "torchaudio" \
        --extra-index-url https://download.pytorch.org/whl/cu121 \
        --force-reinstall

RUN curl -fsSL https://raw.githubusercontent.com/EdgarFuentes-Divelopers/f5tts-runpod-worker/master/.runpod/handler.py \
    -o /handler.py

CMD ["python", "-u", "/handler.py"]