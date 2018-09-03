# Copyright The Helm Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

ARG QEMU_IMAGE=nixm0nk3y/go-build:latest

FROM ${QEMU_IMAGE} as qemu

FROM arm32v6/alpine:3.8 as base
MAINTAINER Nick Gregory <docker@openenterprise.co.uk>

# Enable non-native builds of this image on an amd64 hosts.
# This must be the first RUN command in this file!
# we only need this for the intermediate "base" image, so we can run all the apk and other commands
# when running on a kernel >= 4.8, this will become less relevant
COPY --from=qemu /usr/bin/qemu-arm-static /usr/bin/

RUN apk update && apk add ca-certificates socat && rm -rf /var/cache/apk/*

ENV HOME /tmp

COPY helm /helm
COPY tiller /tiller

EXPOSE 44134
USER nobody
ENTRYPOINT ["/tiller"]

