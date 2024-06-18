FROM golang:1.22 AS builder
WORKDIR /opt/app
COPY . .
RUN go mod tidy && go build -o solana-ping-api

FROM debian:latest
ENV SOLANA_VERSION=1.18.15
RUN apt-get update && \
    apt-get install ca-certificates curl -y
RUN sh -c "$(curl -sSfL https://release.solana.com/v${SOLANA_VERSION}/install)"
ENV PATH="/root/.local/share/solana/install/active_release/bin:$PATH"
WORKDIR /opt/app
COPY --from=builder /opt/app/solana-ping-api /usr/local/bin/solana-ping-api
CMD ["solana-ping-api"]