# dockerfiles/alpine/.common
#
# Dockerfile for Alpine Linux images
ARG BASE_IMAGE
ARG BASE_IMAGE_TAG

FROM $BASE_IMAGE:$BASE_IMAGE_TAG

ARG USR
ARG GRP
ARG UID
ARG GID
ARG COMMIT
ARG BUILD_ID
ARG BUILD_TS
ARG INIT_VERSION
ARG MAINTAINER
ARG LABEL_PREFIX
ARG ALPINE_VERSION

RUN test -n "$USR" && \
    test -n "$GRP" && \
    test -n "$UID" && \
    test -n "$GID" && \
    test -n "$COMMIT" && \
    test -n "$BUILD_ID" && \
    test -n "$BUILD_TS" && \
    test -n "$INIT_VERSION" && \
    test -n "$MAINTAINER" && \
    test -n "$LABEL_PREFIX" && \
    test -n "$ALPINE_VERSION"

LABEL $LABEL_PREFIX.commit=$COMMIT \
      $LABEL_PREFIX.build.id=$BUILD_ID \
      $LABEL_PREFIX.build.ts=$BUILD_TS \
      $LABEL_PREFIX.init.version=$INIT_VERSION \
      $LABEL_PREFIX.maintainer=$MAINTAINER \
      $LABEL_PREFIX.alpine.version=$ALPINE_VERSION

ENV USER=$USR \
    GROUP=$GRP \
    UID=$UID \
    GID=$GID \
    COMMIT=$COMMIT \
    BUILD_ID=$BUILD_ID \
    BUILD_TS=$BUILD_TS \
    INIT_VERSION=$INIT_VERSION \
    MAINTAINER=$MAINTAINER \
    LABEL_PREFIX=$LABEL_PREFIX \
    ALPINE_VERSION=$ALPINE_VERSION \
    LANG=C.UTF-8

RUN apk add --no-cache ca-certificates && \
    wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v${INIT_VERSION}/dumb-init_${INIT_VERSION}_amd64 && \
    chmod +x /usr/local/bin/dumb-init

RUN addgroup -S $GRP -g $GID && \
    adduser -S -G $GRP -u $UID $USR

USER $USR
WORKDIR /home/$USR

ENTRYPOINT ["/usr/local/bin/dumb-init", "--"]
CMD ["/usr/bin/env", "sh"]