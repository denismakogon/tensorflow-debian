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

## Example

Here's the example of a dockerfile that you need to use to build TensorFlow apps 
with Go and package those in Docker container:
```dockerfile
FROM denismakogon/tensorflow-build-stage:edge as build-stage

ADD . /go/src/func/
WORKDIR /go/src/func
RUN dep ensure -v
RUN go build -o func

FROM denismakogon/tensorflow-runtime:edge

COPY --from=build-stage /go/src/func/func /function/func
RUN /function/func

ENTRYPOINT ["/function/func"]

```
