FROM golang:1.22-alpine AS build
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 go build -o devboard-backend .

FROM alpine:3.19
WORKDIR /app
COPY --from=build /app/devboard-backend .
RUN adduser -D -u 10001 app && chown -R app:app /app
USER app
EXPOSE 8080
ENTRYPOINT ["./devboard-backend"]
