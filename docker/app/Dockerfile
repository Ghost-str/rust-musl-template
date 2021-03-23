FROM alpine:latest as bulder
RUN apk add --no-cache gcc musl-dev curl
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > ./tmp/rustup && \
    sh ./tmp/rustup -y && \
    rm -rf ./tmp/rustup
RUN $HOME/.cargo/bin/rustup target add x86_64-unknown-linux-musl

WORKDIR /usr/src/myapp
COPY . .
RUN $HOME/.cargo/bin/cargo build --target x86_64-unknown-linux-musl  --release

FROM scratch

COPY --from=bulder /usr/src/myapp/target/x86_64-unknown-linux-musl/release/rust-musl /

CMD ["/rust-musl"]
