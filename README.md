# Jupyter Polyglot
[![Docker Repository on Quay](https://quay.io/repository/mpfilbin/jupyter-polyglot/status "Docker Repository on Quay")](https://quay.io/repository/mpfilbin/jupyter-polyglot)

Jupyter Polyglot is a Jupyter distribution that supports multiple language kernels. This distribution is ideal for language experimentation, prototyping, or those just learning to program.

## Supported Kernels

1. Python 2
2. Ruby
3. JavaScript
4. Bash
5. Go

## Running Jupyter Polyglot

```shell
docker run -d -p 8888:888 -v /opt/notebooks:<local notebook path> --name jupyter-polyglot quay.io/mpfilbin/jupyter-polyglot:latest
```