# TensorFlow Debian:stretch Docker images

## What's in build-stage image?

 - Debian stretch
 - Golang 1.10
 - Golang dep tool 0.4
 - TensorFlow 1.6.0 runtime (libtensorflow)
 - Build tools (git ,ca-certificates ,openssl ,gcc)

Overall image size: ~658MB

## What's in runtime image?

 - Debian stretch
 - TensorFlow 1.6.0 runtime (libtensorflow)

Overall image size: ~128MB

## Purpose

This is a build image for the multi-stage image provisioning as well as runtime image to work with TensorFlow apps written in Go.

## Example

Sample Docker file you can find [here](example/Dockerfile).

## Build the runtime image

```bash
pushd runtime && docker build -t denismakogon/tensorflow-runtime:edge .; popd
```

## Build the build-stage image

```bash
pushd build-stage && docker build -t denismakogon/tensorflow-build-stage:edge .; popd
```

## Test sample:

```bash
pushd example && docker build -t denismakogon/tensorflow-golang-test:test .;popd
```
