FROM golang:1.23.2-bookworm

WORKDIR /app
COPY go_grpc_bench /app
COPY proto /app/proto

RUN apt update && apt install -y protobuf-compiler
RUN go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.33.0
RUN go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.3.0

RUN protoc -I /app/proto/helloworld /app/proto/helloworld/helloworld.proto --go-grpc_out=/app/ --go_out=/app/
RUN go mod tidy && go build ./... && go install ./...

ENTRYPOINT example
