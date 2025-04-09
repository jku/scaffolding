FROM golang:1.24.1@sha256:52ff1b35ff8de185bf9fd26c70077190cd0bed1e9f16a2d498ce907e5c421268 AS builder
ENV APP_ROOT=/opt/app-root
ENV GOPATH=$APP_ROOT

WORKDIR $APP_ROOT/
ADD go.mod go.sum main.go $APP_ROOT/
RUN go mod download

ARG SERVER_LDFLAGS
RUN go build -ldflags "${SERVER_LDFLAGS}" 
RUN CGO_ENABLED=0 go build -gcflags "all=-N -l" -ldflags "${SERVER_LDFLAGS}" -o fakeoidc

# Multi-Stage production build
FROM golang:1.24.1@sha256:52ff1b35ff8de185bf9fd26c70077190cd0bed1e9f16a2d498ce907e5c421268 as deploy

# Retrieve the binary from the previous stage
COPY --from=builder /opt/app-root/fakeoidc /usr/local/bin/fakeoidc

# Set the binary as the entrypoint of the container
CMD ["fakeoidc"]
