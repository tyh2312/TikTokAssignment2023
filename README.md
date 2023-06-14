# TikTok Backend assignment_2023

![Tests](https://github.com/TikTokTechImmersion/assignment_demo_2023/actions/workflows/test.yml/badge.svg)

## Installation

Requirement:

- golang 1.18+
- docker

To install dependency tools:

```bash
make pre
```
1. Install thrift compiler and Kitex:
```bash
go install github.com/cloudwego/thriftgo
go install github.com/cloudwego/kitex/tool/cmd/kitex@latest
```
2. Generate the code for http-server and rpc-server
```bash
cd ./rpc-server
kitex -module "github.com/TikTokTechImmersion/assignment_demo_2023/rpc-server" -service imservice ../idl_rpc.thrift
cp -r ./kitex_gen ../http-server # copy kitex_gen to http-server
```

For HTTP Server (using Hertz):

1. Install Protobuf
```bash
install protobuf 
```

2. Install the protoc-gen-go plugin for generation of idl code 
```bash
go install github.com/golang/protobuf/protoc-gen-go@latest
```

3. Generate the new API definitions
```bash
protoc --go_out=./http-server/proto_gen/api --go_opt=paths=source_relative ./idl_http.proto
```

Setup Redis by installing the following:

1. Install Redis Go client for rpc-server
```bash
cd ../rpc-server
go get github.com/redis/go-redis/v9
```

## Run

```bash
docker-compose up -d
```

Check if it's running:

```bash
curl localhost:8080/ping
```
