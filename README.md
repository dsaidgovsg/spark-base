# Spark Base Image

![CI Status](https://img.shields.io/github/workflow/status/guangie88/spark-base/CI/master?label=CI&logo=github&style=for-the-badge)

Dockerfile setup for Spark set-up, imbued with varying degree of Python
data science packages.

This set-up is mainly useful for creating Spark workers via Docker containers,
since for Pyspark, the requirements have to be installed on the workers.

All the build arguments variables are template interpolated in from the file
[`templates/vars.yml`](templates/vars.yml), including the set of `pip` packages,
which include the following:

- `numpy`
- `pandas`
- `pendulum==1.4.4`
- `pyjwt`
- `pyproj`
- `shapely`
- `requests`

Note that the versions might not be of the latest, and there are possible
discrepencies between Python 2.7 and Python 3.y due to some of the package
requirements.

## Example Docker build command

```bash
SPARK_VERSION="2.4.4"
SCALA_VERSION="2.12"
HADOOP_VERSION="3.1.0"
PYTHON_VERSION="3.7"
PACKAGE_SET="numpy~=1.11 pandas~=0.23.0 pyjwt~=1.5 pyproj~=1.9 shapely~=1.5 requests~=2.18"

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

Always make changes in `templates/ci.yml.tmpl` since the template will be
applied onto `.github/workflows/ci.yml`.

Run `templates/apply-vars.sh` to apply the template once `tera-cli` has been
installed.
