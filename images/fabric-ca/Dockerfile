#
# Copyright IBM Corp. All Rights Reserved.
#
# SPDX-License-Identifier: Apache-2.0
#
ARG GO_VER
ARG ALPINE_VER

#FROM golang:${GO_VER}-alpine as builder
FROM fabric-golang.local:latest as builder
ARG GO_LDFLAGS
ARG GO_TAGS

#RUN apk add --no-cache \
#	gcc \
#	git \
#	libtool \
#	musl-dev;

ADD . $GOPATH/src/github.com/hyperledger/fabric-ca
RUN go install -tags "${GO_TAGS}" -ldflags "${GO_LDFLAGS}" \
	github.com/hyperledger/fabric-ca/cmd/fabric-ca-server \
	&& go install -tags "${GO_TAGS}" -ldflags "${GO_LDFLAGS}" \
	github.com/hyperledger/fabric-ca/cmd/fabric-ca-client


#FROM alpine:${ALPINE_VER}
FROM fabric-golang.local:latest
#RUN apk add --no-cache \
#	tzdata \
#	libltdl;
ENV FABRIC_CA_HOME /etc/hyperledger/fabric-ca-server
COPY --from=builder /go/bin /usr/local/bin
EXPOSE 7054
CMD fabric-ca-server start -b admin:adminpw
