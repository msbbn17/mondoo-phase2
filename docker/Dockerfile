FROM --platform=linux/amd64 golang:alpine AS getasset

ARG RELEASE_TAG

RUN apk add --no-cache curl tar

ENV ASSET_URL=https://github.com/msbbn17/mondoo-phase1/releases/download/${RELEASE_TAG}/mondoo-challenge-${RELEASE_TAG}-linux-amd64.tar.gz

WORKDIR /app

RUN curl -L $ASSET_URL -o mondoo-webserver.tar.gz && tar -xzf mondoo-webserver.tar.gz && mv mondoo-challenge /app/mondoo-webserver && chmod +x /app/mondoo-webserver
FROM --platform=linux/amd64 alpine:latest

RUN apk add --no-cache libc6-compat

WORKDIR /app

COPY --from=getasset /app/mondoo-webserver /app/mondoo-webserver

EXPOSE 8080
RUN chmod +x mondoo-webserver
ENTRYPOINT ["/app/mondoo-webserver"]