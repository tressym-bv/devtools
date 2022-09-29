FROM ubuntu:latest

ENV RUSTUP_HOME=/usr/local/rustup \
	CARGO_HOME=/usr/local/cargo \
	PATH=/usr/local/cargo/bin:/root/.surrealdb/:$PATH \
    OPENSSL_DIR=/usr/local/ssl/

WORKDIR /usr/local/app

RUN apt update -y
RUN apt-get install -y \
    build-essential \
    checkinstall \
    protobuf-compiler \
    curl wget \
    llvm-14 \
    clang-14 \
    gcc \
    zlib1g-dev

# Install OpenSSL
RUN apt-get install -y libssl-dev

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
RUN rustup target add x86_64-unknown-linux-musl
RUN rustup target add wasm32-unknown-unknown
RUN rustup component add clippy
RUN rustup component add rustfmt
RUN cargo install trunk

# Install Istio
RUN curl -L https://istio.io/downloadIstio | sh -s -- -y
RUN rm -rf istio*

# Install SurrealDB
RUN curl -sSf https://install.surrealdb.com | sh -s -- -y

CMD [ "/bin/bash" ]
