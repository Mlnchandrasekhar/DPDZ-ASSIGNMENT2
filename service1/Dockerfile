FROM golang:1.21-alpine AS builder

WORKDIR /app
COPY . .

# Remove go mod init — it's only needed once when creating the module
RUN go mod tidy
RUN go build -o service1

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /app/service1 .
EXPOSE 8001
CMD ["./service1"]
