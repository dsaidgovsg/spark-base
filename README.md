# Spark Base Image

Experimental Dockerfile setup for Spark set-up, imbued with varying degree of
Python data science packages.

This set-up is mainly useful for creating Spark workers via Docker containers,
since for Pyspark, the requirements have to be installed on the workers.

The following build arguments are:

- `SPARK_VERSION`
  - Currently only `2.4.0` is supported
- `HADDOP_VERSION`
  - Currently only `3.1.0` is supported
- `PACKAGE_SET`
  - Currently only `"standard"` is supported, which includes:
    - `numpy`
    - `pandas`
    - `pyjwt`
    - `pyproj`
    - `shapely`
    - `requests`
