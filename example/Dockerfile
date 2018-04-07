FROM denismakogon/tensorflow-build-stage:edge as build-stage

ADD . /go/src/func/
WORKDIR /go/src/func
RUN dep ensure -v
RUN go build -o func

FROM denismakogon/tensorflow-runtime:edge

COPY --from=build-stage /go/src/func/func /function/func
RUN /function/func

ENTRYPOINT ["/function/func"]
