ARG SPARK_VERSION
ARG SCALA_VERSION
ARG HADOOP_VERSION
ARG PYTHON_VERSION
ARG FROM_DOCKER_IMAGE=guangie88/spark-custom-addons
FROM ${FROM_DOCKER_IMAGE}:${SPARK_VERSION}_scala-${SCALA_VERSION}_hadoop-${HADOOP_VERSION}_python-${PYTHON_VERSION}_hive_pyspark_alpine

ARG PACKAGE_SET=standard

RUN set -euo pipefail && \
    # Install build deps
    apk add --no-cache \
        gcc \
        g++ \
        musl-dev \
        ; \
    # geos-dev only exist in edge/testing unfortunately
    apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing \
        geos \
        geos-dev \
        ; \
    # Install pip packages
    if [ "${PACKAGE_SET}" = "standard" ]; then \
        # Cannot use pandas~=0.22.0 due to Cython C generation issue for Python 3.7
        # https://github.com/pandas-dev/pandas/issues/21785
        PACKAGES="numpy~=1.11 pandas~=0.23.3 pyjwt~=1.5 pyproj~=1.9 shapely~=1.5 requests~=2.18"; \
    fi; \
    python -m pip install --no-cache-dir --no-binary=:all: ${PACKAGES}; \
    # Clean up build deps
    apk del \
        gcc \
        g++ \
        # Only the shared library is required at runtime
        musl-dev \
        geos-dev \
        ; \
    :
