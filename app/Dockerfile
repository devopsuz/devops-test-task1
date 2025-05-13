# Build Stage
FROM golang:1.24-alpine AS builder

WORKDIR /app

COPY . .

RUN go build -o app

# Final Stage
FROM alpine:latest

# Create group and user
RUN addgroup -S task && adduser -S -G task task

# Only copy the build binary
COPY --from=builder /app /app

# Set ownership and permissions
RUN chown -R task:task /app

# Start the container as user
USER task

EXPOSE 3000

CMD ["/app/app"]
