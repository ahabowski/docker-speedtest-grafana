FROM debian:10-slim AS get-speedtest

RUN apt update && apt install curl -y
RUN curl -s https://install.speedtest.net/app/cli/install.deb.sh | bash
RUN apt install speedtest -y


FROM alpine as install-dependencies
RUN apk add --no-cache npm
WORKDIR /build
COPY . .
RUN npm ci

FROM alpine as prod-stage
RUN apk add --no-cache nodejs

WORKDIR /usr/src/app

CMD [ "node", "index.js" ]

COPY --from=get-speedtest /usr/bin/speedtest /usr/bin/speedtest
COPY --from=install-dependencies /build .
