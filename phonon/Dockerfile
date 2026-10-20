ARG BUILD_FROM
ARG PTTS_VERSION=0.4.0

# The server is the published ptts-openai-server image's: built once by xn-ptts' CI, so
# installing the app compiles nothing on the device.
FROM ghcr.io/gradium-ai/ptts-openai-server:${PTTS_VERSION} AS ptts

FROM ${BUILD_FROM}

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN apt-get update \
    && apt-get install -y --no-install-recommends ca-certificates libmp3lame0 libopus0 \
    && rm -rf /var/lib/apt/lists/*

# The binary, and on amd64 its two builds and the script that picks one for the CPU.
COPY --from=ptts /usr/local/ /usr/local/
COPY rootfs /

# A Wyoming round trip, not just an open port.
HEALTHCHECK --start-period=30m --interval=30s --timeout=10s --retries=3 \
    CMD bash -c 'exec 3<>/dev/tcp/127.0.0.1/10200 \
        && printf "{\"type\": \"describe\"}\n" >&3 \
        && timeout 5 head -c 1 <&3 > /dev/null'
