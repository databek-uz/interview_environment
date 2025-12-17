# Use Python base image instead of Bitnami Spark to avoid pull issues
FROM python:3.11-slim-bookworm

USER root

# Install system dependencies
RUN apt-get update && apt-get install -y \
    openjdk-17-jdk \
    wget \
    curl \
    git \
    procps \
    && rm -rf /var/lib/apt/lists/*

# Set Java environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$PATH:$JAVA_HOME/bin

# Install Spark 3.5.1
ENV SPARK_VERSION=3.5.1
ENV HADOOP_VERSION=3
ENV SPARK_HOME=/opt/spark
ENV PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
ENV PYSPARK_PYTHON=python3

# Download and install Spark with progress indicator
RUN echo "Downloading Apache Spark ${SPARK_VERSION} (~400MB)..." && \
    wget --progress=bar:force:noscroll \
    https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    echo "Extracting Spark..." && \
    tar -xzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} ${SPARK_HOME} && \
    rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    echo "Spark installation completed!"

# Install Python packages
RUN echo "Installing Python packages..." && \
    pip install --no-cache-dir \
    pyspark==${SPARK_VERSION} \
    pandas \
    numpy \
    pyarrow \
    jupyter \
    ipykernel \
    matplotlib \
    debugpy \
    findspark && \
    echo "Python packages installed!"

# Create non-root user for development
RUN useradd -m -s /bin/bash vscode && \
    mkdir -p /workspace && \
    chown -R vscode:vscode /workspace

USER vscode
WORKDIR /workspace
