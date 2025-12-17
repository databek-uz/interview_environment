FROM bitnami/spark:3.0.0

USER root

# Python libs + tools
RUN pip install --no-cache-dir \
    pandas \
    numpy \
    pyarrow \
    jupyter \
    ipykernel \
    matplotlib \
    debugpy

WORKDIR /workspace
