FROM ghcr.io/swivid/f5-tts:main

RUN pip install --no-cache-dir runpod

COPY handler.py /handler.py

CMD ["python", "-u", "/handler.py"]