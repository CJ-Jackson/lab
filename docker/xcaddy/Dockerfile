FROM docker.io/golang:1.26.4-alpine3.23 AS builder

RUN adduser -D builder
USER builder
WORKDIR /home/builder

ENV GOPATH="/home/builder/go" XCADDY_VERSION="v0.4.5"
RUN go install "github.com/caddyserver/xcaddy/cmd/xcaddy@${XCADDY_VERSION}"

ENV CADDY_VERSION="v2.11.4" CLOUDFLARE_REV="a8737d095ad5a48ca031cea6ab704057dbc2d250" GOOS="linux" GOARCH="amd64"

RUN go/bin/xcaddy build "${CADDY_VERSION}" --output caddy \
  --with "github.com/caddy-dns/cloudflare@${CLOUDFLARE_REV}" && echo "caddy-x64-${CADDY_VERSION}" > caddy-x64.txt

FROM docker.io/alpine:3.23

COPY caddy-to-output /usr/local/bin/caddy-to-output
RUN chmod +x /usr/local/bin/caddy-to-output && adduser -S caddy
USER caddy

COPY --from=builder /home/builder/caddy /usr/local/bin/caddy
COPY --from=builder /home/builder/caddy-x64.txt /opt/caddy-x64.txt

CMD ["caddy"]
