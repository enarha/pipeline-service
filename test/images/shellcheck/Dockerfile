#FROM registry.access.redhat.com/ubi8/ubi-minimal:8.6
FROM registry.access.redhat.com/ubi8/ubi-minimal@sha256:e58664de16551db29fb0eaaeb3c4a44eaf95ad89a5b2399a1107041c4f2d6d34
LABEL build-date= \
    com.redhat.build-host= \
    description="This image provides shellcheck binary." \
    distribution-scope="public" \
    io.k8s.description="This image provides shellcheck binary." \
    io.k8s.display-name="shellcheck" \
    maintainer="Pipeline Service" \
    name="shellcheck" \
    release="0.1" \
    summary="Provides the 0.8.0 shellcheck" \
    url="https://github.com/openshift-pipelines/pipeline-service/tree/main/images/shellcheck" \
    vcs-ref=  \
    vcs-type="git" \
    vendor="Pipeline Service" \
    version="0.1"
WORKDIR /
RUN mkdir /workspace && chmod 777 /workspace && chown 65532:65532 /workspace
ENV HOME /tmp/home
RUN mkdir $HOME && chmod 777 $HOME && chown 65532:65532 $HOME
RUN microdnf install -y tar-1.30 xz-5.2.4 findutils-4.6.0 && microdnf clean all
RUN SHELLCHECK_VERSION=v0.8.0 && \
    curl -L -o /tmp/shellcheck.tar.xz "https://github.com/koalaman/shellcheck/releases/download/$SHELLCHECK_VERSION/shellcheck-$SHELLCHECK_VERSION.linux.x86_64.tar.xz" && \
    tar -xJvf /tmp/shellcheck.tar.xz -C /tmp && \
    mv /tmp/shellcheck-$SHELLCHECK_VERSION/shellcheck /usr/local/bin/shellcheck && \
    chmod 755 /usr/local/bin/shellcheck && \
    shellcheck -V
USER 65532:65532
VOLUME /workspace
WORKDIR /workspace