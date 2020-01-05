ARG BASE_VERSION
ARG SPARK_VERSION
ARG SCALA_VERSION
ARG HADOOP_VERSION
ARG PYTHON_VERSION
ARG FROM_DOCKER_IMAGE=guangie88/spark-custom-addons
FROM ${FROM_DOCKER_IMAGE}:${BASE_VERSION}_${SPARK_VERSION}_scala-${SCALA_VERSION}_hadoop-${HADOOP_VERSION}_python-${PYTHON_VERSION}_hive_pyspark_alpine

ARG PACKAGE_SET

RUN set -euo pipefail && \
    # Install build deps
    apk add --no-cache \
        gcc \
        g++ \
        musl-dev \
        ; \
    # geos-dev only exist in edge/community unfortunately
    apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community \
        geos \
        geos-dev \
        ; \
    # Install pip packages
    python -m pip install --no-cache-dir --no-binary=:all: Cython; \
    python -m pip install --no-cache-dir --no-binary=:all: ${PACKAGE_SET}; \
    # Clean up build deps
    apk del \
        gcc \
        g++ \
        # Only the shared library is required at runtime
        musl-dev \
        geos-dev \
        ; \
    :
