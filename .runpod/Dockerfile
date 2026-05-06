FROM ghcr.io/swivid/f5-tts:main

RUN pip install --no-cache-dir runpod

RUN curl -fsSL https://raw.githubusercontent.com/EdgarFuentes-Divelopers/f5tts-runpod-worker/master/.runpod/handler.py \
    -o /handler.py

CMD ["python", "-u", "/handler.py"]