FROM rust:latest as bulder

WORKDIR /usr/src/myapp
COPY . .
RUN rustup target add x86_64-unknown-linux-musl
RUN cargo build --target x86_64-unknown-linux-musl  --release

FROM scratch

COPY --from=bulder /usr/src/myapp/target/x86_64-unknown-linux-musl/release/rust-musl /

CMD ["/rust-musl"]
