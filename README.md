# Jupyter Polyglot
[![Docker Repository on Quay](https://quay.io/repository/mpfilbin/jupyter-polyglot/status "Docker Repository on Quay")](https://quay.io/repository/mpfilbin/jupyter-polyglot)

Jupyter Polyglot is a Jupyter distribution that supports multiple language kernels. This distribution is ideal for language experimentation, prototyping, or those just learning to program.

**Notice:** This project has moved to: https://scm.filb.in/mfilbin/polyglot-jupyter-notebook

## Supported Kernels

1. Python 2
2. Ruby
3. JavaScript
4. Bash
5. Go

## Running Jupyter Polyglot

```shell
docker run -d \
  -p 8888:8888 \
  -v $(pwd):/opt/notebooks \
  --name jupyter-polyglot \
  quay.io/mpfilbin/jupyter-polyglot:latest
```
