FROM caddy:2.11.7-builder-alpine AS builder

ARG CADDY_VERSION=v2.11.7
ARG CROWDSEC_BOUNCER_VERSION=v0.14.1
ARG CADDY_L4_VERSION=v0.1.2
ARG TRANSFORM_ENCODER_VERSION=v0.0.0-20260423033309-ba4124974830

RUN xcaddy build ${CADDY_VERSION} \
    --with github.com/mholt/caddy-l4@${CADDY_L4_VERSION} \
    --with github.com/caddyserver/transform-encoder@${TRANSFORM_ENCODER_VERSION} \
    --with github.com/hslatman/caddy-crowdsec-bouncer/http@${CROWDSEC_BOUNCER_VERSION} \
    --with github.com/hslatman/caddy-crowdsec-bouncer/appsec@${CROWDSEC_BOUNCER_VERSION} \
    --with github.com/hslatman/caddy-crowdsec-bouncer/layer4@${CROWDSEC_BOUNCER_VERSION}

FROM caddy:2.11.7

COPY --from=builder /usr/bin/caddy /usr/bin/caddy

RUN setcap cap_net_bind_service=+ep /usr/bin/caddy
