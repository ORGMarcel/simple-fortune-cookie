# Stage 1: Build the Go application
FROM golang:1.18-alpine AS builder

# Set the working directory
WORKDIR /app

# Copy the Go modules files and download dependencies
COPY go.mod ./
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application
RUN go build -o main .

# Stage 2: Run the application
FROM alpine:latest

# Set the working directory
WORKDIR /app

# Copy the built binary from the builder stage
COPY --from=builder /app/main .

# Expose the application port (if needed)
EXPOSE 8080

# Copy templates and static files to the working directory
COPY --from=builder /app/templates /app/templates
COPY --from=builder /app/static /app/static

# Run the application
CMD ["./main"]
