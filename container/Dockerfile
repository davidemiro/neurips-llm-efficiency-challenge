FROM pytorch/pytorch:2.1.0-cuda12.1-cudnn8-devel

RUN apt-get update  && apt-get install -y git python3-virtualenv wget

RUN pip install -q -U git+https://github.com/huggingface/transformers.git
RUN pip install -q -U git+https://github.com/huggingface/peft.git
RUN pip install -q -U git+https://github.com/huggingface/accelerate.git
RUN pip install trl datasets

WORKDIR /workspace
# Setup server requriements
COPY ./fast_api_requirements.txt fast_api_requirements.txt
RUN pip install --no-cache-dir --upgrade -r fast_api_requirements.txt

ENV HUGGINGFACE_TOKEN="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"
ENV HUGGINGFACE_REPO="mistralai/Mistral-7B-v0.1"

# Copy over single file server
COPY ./inference.py inference.py
COPY ./api.py api.py
# Run the server
CMD ["uvicorn", "inference:app", "--host", "0.0.0.0", "--port", "80"]
