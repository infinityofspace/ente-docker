# syntax=docker/dockerfile:1
FROM node:21-bookworm-slim as ente-builder

WORKDIR /app
RUN apt update && apt install -y ca-certificates && rm -rf /var/lib/apt/lists/*

COPY . .
RUN yarn install
ENV NEXT_PUBLIC_ENTE_ENDPOINT=DOCKER_RUNTIME_REPLACE_ENDPOINT
ENV NEXT_PUBLIC_ENTE_ALBUMS_ENDPOINT=DOCKER_RUNTIME_REPLACE_ALBUMS_ENDPOINT
RUN yarn build

FROM nginx:1.25-alpine-slim
COPY --from=ente-builder /app/apps/photos/out /usr/share/nginx/html
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

ARG ENDPOINT="http://localhost:8080"
ENV ENDPOINT="$ENDPOINT"
ARG ALBUMS_ENDPOINT="http://localhost:8082"
ENV ALBUMS_ENDPOINT="$ALBUMS_ENDPOINT"

COPY replace_ente_endpoints.sh /docker-entrypoint.d/replace_ente_endpoints.sh

RUN chmod +x /docker-entrypoint.d/replace_ente_endpoints.sh
