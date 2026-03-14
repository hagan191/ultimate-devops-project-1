FROM golang:1.22-alpine AS builder

WORKDIR /usr/src/app

# Copy only dependency files first
COPY go.mod go.sum ./
RUN go mod download

# Then copy rest of the code
COPY . .

RUN go build -o product-catalog ./

FROM alpine AS release

WORKDIR /usr/src/app

COPY ./products ./products
COPY --from=builder /usr/src/app/product-catalog ./

EXPOSE 8080

ENV PRODUCT_CATALOG_PORT=8080
ENTRYPOINT ["./product-catalog"]









