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
        cmake \
        gcc \
        git \
        g++ \
        make \
        musl-dev \
        ; \
    # Install geos packages
    git clone --depth=1 https://github.com/libgeos/geos.git -b 3.8.0; \
    cd geos; \
    cmake -DCMAKE_BUILD_TYPE=Release .; \
    make -j 4; \
    make install; \
    cd -; \
    rm -rf geos; \
    ldconfig /usr/local/lib/; \
    # Install pip packages
    python -m pip install --no-cache-dir Cython; \
    python -m pip install --no-cache-dir numpy~=1.17; \
    python -m pip install --no-cache-dir ${PACKAGE_SET}; \
    # Clean up build deps
    apk del \
        cmake \
        gcc \
        git \
        g++ \
        make \
        # Only the shared library is required at runtime
        musl-dev \
        ; \
    :
