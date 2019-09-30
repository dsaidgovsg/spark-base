ARG SPARK_VERSION
ARG SCALA_VERSION
ARG HADOOP_VERSION
ARG PYTHON_VERSION
ARG FROM_DOCKER_IMAGE=guangie88/spark-custom-addons
FROM ${FROM_DOCKER_IMAGE}:${SPARK_VERSION}_scala-${SCALA_VERSION}_hadoop-${HADOOP_VERSION}_python-${PYTHON_VERSION}_hive_pyspark_debian

ARG PACKAGE_SET=standard

RUN set -euo pipefail && \
    # Install build deps
    PYTHON_MAJOR_VERSION="$(python3 2>&1 --version | cut -d " " -f 2 | cut -d "." -f 1)"; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        build-essential \
        libgeos-dev \
        ; \
    # Install pip packages - the left-to-right order matters
    if [ "${PACKAGE_SET}" = "standard" ]; then \
        # Cannot use pandas~=0.22.0 due to Cython C generation issue for Python 3.7
        # https://github.com/pandas-dev/pandas/issues/21785
        PACKAGES="numpy~=1.11 pandas~=0.23.0 pyjwt~=1.5 pyproj~=1.9 shapely~=1.5 requests~=2.18"; \
    fi; \
    python -m pip install --no-cache-dir --no-binary=:all: ${PACKAGES}; \
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
