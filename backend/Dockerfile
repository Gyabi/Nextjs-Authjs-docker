# Rustのマルチステージビルド用Dockerfile

FROM rust:1.71 AS base

# 開発ステージ
FROM base AS dev

WORKDIR /backend
COPY . .

# ビルドステージ
FROM dev AS builder

RUN ["cargo", "build", "--release"]

# 本番ステージ
FROM debian:12-slim AS prod

WORKDIR /backend

COPY --from=builder /backend/target/release/backend ./backend

CMD [ "./backend" ]