# Build Stage
FROM caddy:builder-alpine AS builder

RUN xcaddy build \
    --with github.com/caddy-dns/cloudflare

# Runtime Stage (Lightweight)
FROM caddy:2-alpine

COPY --from=builder /usr/bin/caddy /usr/bin/caddy
