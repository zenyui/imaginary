VERSION 0.7

FROM golang:1.17-bullseye

submodule:
    WORKDIR /app
    COPY --dir ./imaginary/ .
    RUN ls -la
    SAVE ARTIFACT ./imaginary /imaginary

build-image:
    FROM DOCKERFILE -f +submodule/imaginary/Dockerfile +submodule/imaginary/*

build-production:
    FROM +build-image
    ARG VERSION=dev
    SAVE IMAGE --push ghcr.io/zenyui/imaginary:${VERSION}

all:
    # BUILD +build-production
    BUILD +build-testing-ci

build-testing-ci:
    FROM +submodule
    ARG VERSION=dev
    SAVE IMAGE --push ghcr.io/zenyui/imaginary:${VERSION}
