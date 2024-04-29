# Nextjsのマルチステージビルド用Dockerfile

FROM node:18-alpine AS base


# 開発ステージ
FROM base AS dev

WORKDIR /app
COPY package.json package-lock.json ./

RUN npm install

COPY . .

# ビルドステージ
FROM dev AS builder

RUN ["npm", "run", "build"]
# 本番ステージ
FROM base AS prod

WORKDIR /app

# standaloneモードに必要なファイルをすべてコピー
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next/static ./.next/static
COPY --from=builder /app/.next/standalone ./

CMD [ "node", "server.js" ]

