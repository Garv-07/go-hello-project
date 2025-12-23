# Build stage
FROM golang:1.22-alpine AS builder
WORKDIR /app
COPY app/go.mod .
RUN go mod download
COPY app/ .
RUN go build -o hello

# Runtime stage
FROM alpine:latest
WORKDIR /root/
COPY --from=builder /app/hello .
EXPOSE 8080
CMD ["./hello"]
