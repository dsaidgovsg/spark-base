ARG BASE_VERSION
ARG SPARK_VERSION
ARG SCALA_VERSION
ARG HADOOP_VERSION
ARG PYTHON_VERSION
ARG FROM_DOCKER_IMAGE=dsaidgovsg/spark-custom-addons
FROM ${FROM_DOCKER_IMAGE}:${BASE_VERSION}_${SPARK_VERSION}_scala-${SCALA_VERSION}_hadoop-${HADOOP_VERSION}_python-${PYTHON_VERSION}_hive_pyspark_debian

ARG PACKAGE_SET

RUN set -euo pipefail && \
    # Install build deps
    apt-get update; \
    apt-get install -y --no-install-recommends \
        build-essential \
        libgeos-dev \
        ; \
    python -m pip install --no-cache-dir ${PACKAGE_SET}; \
    # Add required runtime libraries
    apt-get install -y --no-install-recommends \
        libgeos-c1v5 \
        ; \
    # Clean up build deps
    apt-get remove -y \
        build-essential \
        libgeos-dev \
        ; \
    apt-get autoremove -y; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*; \
    :
