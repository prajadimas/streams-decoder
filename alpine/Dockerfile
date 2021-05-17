FROM ekidd/rust-musl-builder:stable as builder

RUN USER=root cargo new --bin streams_decoder
WORKDIR ./streams_decoder
ADD . ./
# COPY ./Cargo.lock ./Cargo.lock
# COPY ./Cargo.toml ./Cargo.toml
# COPY ./src/* ./src/
RUN cargo build --release
RUN sudo rm src/*.rs

ADD . ./

RUN sudo rm ./target/x86_64-unknown-linux-musl/release/deps/streams_decoder*
RUN cargo build --release


FROM alpine:latest

ARG APP=/usr/src/app

EXPOSE 8585

ENV TZ=Etc/UTC \
    APP_USER=appuser

RUN addgroup -S $APP_USER \
    && adduser -S -g $APP_USER $APP_USER

RUN apk update \
    && apk add --no-cache ca-certificates tzdata \
    && rm -rf /var/cache/apk/*

COPY --from=builder /home/rust/src/streams_decoder/target/x86_64-unknown-linux-musl/release/streams_decoder ${APP}/streams_decoder
ADD ./config.json ${APP}/

RUN chown -R $APP_USER:$APP_USER ${APP}

USER $APP_USER
WORKDIR ${APP}

CMD ["./streams_decoder"]
