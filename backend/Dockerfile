FROM dhi.io/golang:1-alpine AS builder

USER root

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 go build -ldflags="-s -w" -o devboard-backend .

FROM dhi.io/golang:1-alpine

WORKDIR /app

COPY --from=builder /app/devboard-backend ./devboard-backend

RUN chmod +x ./devboard-backend

USER nonroot

EXPOSE 8080

ENTRYPOINT ["./devboard-backend"]