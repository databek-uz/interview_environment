FROM bitnami/spark:3.5.1-debian-12

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
