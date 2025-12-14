# PulseCheck APIs

Protobuf definitions for PulseCheck microservices.

## Overview

This repository contains the gRPC/Protobuf API definitions for:
- **Monitor Service** - Create and retrieve monitor configurations
- **Checker Service** - Perform URL health checks

## Structure

```
apis/
├── checker/v1/
│   ├── checker.proto
│   ├── checker.pb.go
│   └── checker_grpc.pb.go
└── monitor/v1/
    ├── monitor.proto
    ├── monitor.pb.go
    └── monitor_grpc.pb.go
```

## Prerequisites

- Go 1.25+
- Protocol Buffers compiler (`protoc`)
- Go protobuf plugins:
  ```bash
  go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
  go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
  ```

## Installation

```bash
go get github.com/impruthvi/pulse-check-apis@latest
```

## Regenerating Code

If you modify the `.proto` files, regenerate the Go code:

```bash
# For checker service
protoc --go_out=. --go_opt=paths=source_relative \
  --go-grpc_out=. --go-grpc_opt=paths=source_relative \
  checker/v1/checker.proto

# For monitor service
protoc --go_out=. --go_opt=paths=source_relative \
  --go-grpc_out=. --go-grpc_opt=paths=source_relative \
  monitor/v1/monitor.proto
```

Or use the Makefile:

```bash
make generate
```

## Usage

Import in your Go projects:

```go
import (
    checker "github.com/impruthvi/pulse-check-apis/checker/v1"
    monitor "github.com/impruthvi/pulse-check-apis/monitor/v1"
)
```

## API Documentation

### Monitor Service

- `CreateMonitor` - Register a new URL for monitoring
- `GetMonitor` - Retrieve monitor status and details

### Checker Service

- `CheckURL` - Perform a health check on a URL
