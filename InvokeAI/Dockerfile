FROM python:3.11 

WORKDIR /app 

COPY ./codebase .

RUN apt-get update && apt-get install -y libgl1 curl

# Skipping the installation of bitsandbytes due to Darwin platform incompatibility
RUN sed -i '/"bitsandbytes.*"/d' pyproject.toml

RUN pip install -e ".[dev]"
RUN pip install -e ".[test]"

# Fix onnxruntime binary incompatibility with kernel security settings
RUN pip install "onnxruntime>=1.17.0"

ENTRYPOINT ["invokeai-web"]