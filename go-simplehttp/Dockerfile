FROM golang:1.13-alpine@sha256:8cc699270cfeed0864420e5c650aa9c1b51ed5b23cf927ab4c5eea47f6c0c1a8 AS builder

# Set necessary environmet variables needed for our image
ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64

# Move to working directory /build
WORKDIR /build

# Copy the code into the container
COPY ./simpleHTTP.go .

# Build the application
RUN go build -o simpleHTTP ./simpleHTTP.go

# Move to /dist directory as the place for resulting binary folder
WORKDIR /dist

# Copy binary from build to main folder
RUN cp /build/simpleHTTP .

EXPOSE 6000

# Build a small image
FROM scratch
COPY --from=builder /dist/simpleHTTP /
ENTRYPOINT ["/simpleHTTP"]

