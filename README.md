# Spark Base Image

Experimental Dockerfile setup for Spark set-up, imbued with varying degree of
Python data science packages.

This set-up is mainly useful for creating Spark workers via Docker containers,
since for Pyspark, the requirements have to be installed on the workers.

- `PACKAGE_SET`
  - Currently only `"standard"` is supported, which includes:
    - `numpy`
    - `pandas`
    - `pyjwt`
    - `pyproj`
    - `shapely`
    - `requests`

The other variables are template interpolated in from the file
[`templates/vars.yml`](templates/vars.yml).

## Example Docker build command

```bash
SPARK_VERSION="2.4.4"
SCALA_VERSION="2.12"
HADOOP_VERSION="3.1.0"
PYTHON_VERSION="3.7"
PACKAGE_SET="standard"

docker build debian/ -t spark-base-debian \
    --build-arg "SPARK_VERSION=${SPARK_VERSION}" \
    --build-arg "SCALA_VERSION=${SCALA_VERSION}" \
    --build-arg "HADOOP_VERSION=${HADOOP_VERSION}" \
    --build-arg "PYTHON_VERSION=${PYTHON_VERSION}" \
    --build-arg "PACKAGE_SET=${PACKAGE_SET}"
```

## How to Apply Travis Template

For Linux user, you can download Tera CLI v0.2 at
<https://github.com/guangie88/tera-cli/releases> and place it in `PATH`.

Otherwise, you will need `cargo`, which can be installed via
[rustup](https://rustup.rs/).

Once `cargo` is installed, simply run `cargo install tera-cli --version=^0.2.0`.
