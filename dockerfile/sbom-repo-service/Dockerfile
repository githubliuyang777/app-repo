FROM bitnami/git
RUN git clone https://github.com/opensourceways/sbom-tools.git

FROM golang:1.18.4-alpine3.16 AS builder
WORKDIR /syft
COPY --from=0 /sbom-tools/sbom-generator /syft
RUN CGO_ENABLED=0 go build -o /syft/openeuler-sbom-tools -a -ldflags '-extldflags "-static"' cmd/syft/main.go

FROM openeuler/openeuler:22.03-lts AS final
COPY --from=builder /syft/openeuler-sbom-tools /opt/openeuler-sbom-tools

RUN yum update -y && yum install -y \
    git \
    java-18-openjdk \
    && rm -rf /var/cache/yum

WORKDIR /opt
RUN git clone https://github.com/opensourceways/sbom-repo-service.git

EXPOSE 15551

ENTRYPOINT ["/bin/bash", "/opt/sbom-repo-service/docker-entrypoint.sh"]