FROM ubuntu:latest

ENV RUSTUP_HOME=/usr/local/rustup \
	CARGO_HOME=/usr/local/cargo \
	PATH=/usr/local/cargo/bin:/root/.surrealdb/:$PATH

WORKDIR /usr/local/app

RUN apt update -y
RUN apt-get install -y \
    libprotoc-dev \
    libprotobuf-dev \
    curl \
    llvm-14 \
    clang-14


RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
RUN rustup target add x86_64-unknown-linux-musl
RUN rustup component add clippy
RUN rustup component add rustfmt

RUN curl -L https://istio.io/downloadIstio | sh -s -- -y

RUN curl -sSf https://install.surrealdb.com | sh -s -- -y

CMD [ "/bin/bash" ]
