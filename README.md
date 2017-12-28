# Jupyter Polyglot

Jupyter Polyglot is a Docker image that provides multiple programming language kernels. 

## Supported Kernels

1. Python 2
2. Ruby
3. JavaScript
4. Bash
5. Go

## Running Jupyter Polyglot

```shell
docker run -d -p 8888:888 -v /opt/notebooks:<local notebook path> --name jupyter-polyglot quay.io/mfilbin/jupyter-polyglot
```