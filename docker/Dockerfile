
ARG NODEJS_VERSION 22

FROM node:${NODEJS_VERSION}-alpine as base

ARG POSTGRES_HOST POSTGRES_PORT POSTGRES_USER POSTGRES_DB

RUN apk add --no-cache openssl

WORKDIR /src

COPY package.json pnpm-lock.yaml ./

ENV NODE_ENV development

RUN npm i -g corepack && pnpm install --frozen-lockfile

COPY prisma/schema.prisma ./prisma/schema.prisma

ARG POSTGRES_HOST POSTGRES_PORT POSTGRES_USER POSTGRES_DB
ENV DATABASE_URL "postgres://${POSTGRES_USER}@${POSTGRES_HOST}:${POSTGRES_PORT}/${POSTGRES_DB}?schema=public"

ENV NEXT_TELEMETRY_DISABLED 1

CMD ["sh", "-c", "npx prisma generate && npx prisma studio & pnpm dev"]
