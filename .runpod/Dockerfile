FROM ghcr.io/swivid/f5-tts:main

RUN pip install --no-cache-dir runpod

RUN cat > /handler.py << 'PYEOF'
import runpod
import base64
import tempfile
import os
import subprocess


def handler(job):
    job_input = job.get("input", {})
    text = job_input.get("text", "")
    speed = job_input.get("speed", 1.0)
    remove_silence = job_input.get("remove_silence", True)

    if not text:
        return {"error": "Campo 'text' requerido"}

    with tempfile.NamedTemporaryFile(suffix=".wav", delete=False) as tmp:
        output_path = tmp.name

    try:
        cmd = [
            "f5-tts_infer-cli",
            "--model", os.getenv("MODEL_NAME", "F5TTS_v1_Base"),
            "--gen_text", text,
            "--output_dir", os.path.dirname(output_path),
            "--output_file", os.path.basename(output_path),
            "--speed", str(speed),
        ]
        if remove_silence:
            cmd.append("--remove_silence")

        result = subprocess.run(cmd, capture_output=True, text=True, timeout=300)

        if result.returncode != 0:
            return {"error": result.stderr}

        with open(output_path, "rb") as f:
            audio_b64 = base64.b64encode(f.read()).decode("utf-8")

        return {"audio_base64": audio_b64, "status": "success"}

    except Exception as e:
        return {"error": str(e)}
    finally:
        if os.path.exists(output_path):
            os.unlink(output_path)


runpod.serverless.start({"handler": handler})
PYEOF

CMD ["python", "-u", "/handler.py"]