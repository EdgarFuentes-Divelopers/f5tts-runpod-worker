FROM ghcr.io/swivid/f5-tts:main

# Congelar todos los paquetes instalados como constraints
# Esto impide que runpod actualice torch/torchaudio
RUN pip freeze | grep -v "^-e " > /constraints.txt && \
    pip install --no-cache-dir runpod --constraint /constraints.txt

RUN curl -fsSL https://raw.githubusercontent.com/EdgarFuentes-Divelopers/f5tts-runpod-worker/master/.runpod/handler.py \
    -o /handler.py

CMD ["python", "-u", "/handler.py"]