FROM bitnami/git
RUN git clone https://github.com/zejun19/syft.git

FROM golang:1.18.4-alpine3.16 AS builder
WORKDIR /syft
COPY --from=0 /syft /syft

RUN CGO_ENABLED=0 go build -o /syft/openeuler-sbom-tools -a -ldflags '-extldflags "-static"' cmd/syft/main.go

FROM openeuler/openeuler:22.03-lts AS final
COPY --from=builder /syft/openeuler-sbom-tools /opt/openeuler-sbom-tools
