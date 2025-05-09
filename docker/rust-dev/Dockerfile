FROM rust:1.85-alpine

ARG TARGETOS
ARG TARGETARCH

ENV BUILDX_ARCH="${TARGETOS:-linux}-${TARGETARCH:-amd64}"
ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH

RUN echo "Building for $BUILDX_ARCH"

RUN apk add --no-cache musl-dev libc-dev pkgconfig openssl \
    protoc protobuf-dev openssl-dev git perl make

# Add rust dependencies
RUN if [ "$BUILDX_ARCH" = "linux-arm64" ]; then \
        ARCHITECTURE=aarch64-unknown-linux-musl; \
        else ARCHITECTURE=x86_64-unknown-linux-musl; \
    fi && \
    rustup target add ${ARCHITECTURE} && \
    # Add cross compilation targets
    rustup target add aarch64-apple-ios && \
    rustup target add aarch64-linux-android && \
    rustup target add wasm32-unknown-unknown && \
    rustup component add clippy && \
    rustup component add rustfmt && \
    wget https://github.com/xd009642/tarpaulin/releases/download/0.25.1/cargo-tarpaulin-${ARCHITECTURE}.tar.gz && \
    tar axvf cargo-tarpaulin-${ARCHITECTURE}.tar.gz && \
    mv cargo-tarpaulin $CARGO_HOME/bin/ && \
    rm cargo-tarpaulin-${ARCHITECTURE}.tar.gz

RUN cargo install --locked cargo-deny cargo-about flamegraph

WORKDIR /usr/src/app
