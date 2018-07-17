# dockerfiles/ruby
#
# Dockerfile for Ruby
ARG REPO
ARG BASE_IMAGE
ARG TAG=latest

FROM $REPO/$BASE_IMAGE:$TAG

ARG LABEL_PREFIX
ARG RUBY_VERSION
ARG RUBY_GEM_VERSION
ARG GEMS_VERSION
ARG BUNDLER_VERSION
ARG ALPINE_RUBY_PACKAGE_NAME
ARG ALPINE_RUBY_PACKAGE_VERSION

RUN test -n "$LABEL_PREFIX" && \
    test -n "$RUBY_VERSION" && \
    test -n "$RUBY_GEM_VERSION" && \
    test -n "$GEMS_VERSION" && \
    test -n "$BUNDLER_VERSION" && \
    test -n "$ALPINE_RUBY_PACKAGE_NAME" && \
    test -n "$ALPINE_RUBY_PACKAGE_VERSION"

LABEL $LABEL_PREFIX.ruby.version=$RUBY_VERSION \
      $LABEL_PREFIX.ruby.gem.version=$RUBY_GEM_VERSION \
      $LABEL_PREFIX.gems.version=$GEMS_VERSION \
      $LABEL_PREFIX.bundler.version=$BUNDLER_VERSION \
      $LABEL_PREFIX.alpine.ruby.package.name=$ALPINE_RUBY_PACKAGE_NAME \
      $LABEL_PREFIX.alpine.ruby.package.version=$ALPINE_RUBY_PACKAGE_VERSION

ENV RUBY_VERSION=$RUBY_VERSION \
    RUBY_GEM_VERSION=$RUBY_GEM_VERSION \
    GEMS_VERSION=$GEMS_VERSION \
    BUNDLER_VERSION=$BUNDLER_VERSION \
    ALPINE_RUBY_PACKAGE_NAME=$ALPINE_RUBY_PACKAGE_NAME \
    ALPINE_RUBY_PACKAGE_VERSION=$ALPINE_RUBY_PACKAGE_VERSION

RUN echo "gem: --no-ri --no-rdoc --no-document --no-suggestions --user-install" > /home/$USER/.gemrc

USER root

RUN apk add --no-cache $ALPINE_RUBY_PACKAGE_NAME="$ALPINE_RUBY_PACKAGE_VERSION" ruby-json ruby-irb && \
    gem update --no-document --system $GEMS_VERSION

ENV PATH=$PATH:/home/$USER/.gem/ruby/$RUBY_GEM_VERSION/bin

USER $USER

RUN gem install bundler --force --version $BUNDLER_VERSION