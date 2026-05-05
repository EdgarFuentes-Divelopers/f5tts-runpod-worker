FROM ghcr.io/swivid/f5-tts:main

# --no-deps evita que pip resuelva dependencias y sobreescriba torch/torchaudio
RUN pip install --no-cache-dir runpod --no-deps && \
    pip install --no-cache-dir \
        aiohttp \
        boto3 \
        requests \
        websockets \
        fastapi \
        uvicorn

RUN curl -fsSL https://raw.githubusercontent.com/EdgarFuentes-Divelopers/f5tts-runpod-worker/master/.runpod/handler.py \
    -o /handler.py

CMD ["python", "-u", "/handler.py"]