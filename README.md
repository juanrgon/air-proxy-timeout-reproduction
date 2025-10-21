# Air Proxy Timeout Reproduction

This repository demonstrates the timeout issue with Air's proxy feature when an application takes longer to start up.

## Issue

This repo reproduces the error reported in [air-verse/air#732](https://github.com/air-verse/air/issues/732).

The server has a 1-second delay before starting, which causes Air's proxy to timeout before the application is ready to accept connections.

## Setup

1. Install Air:
   ```bash
   go install github.com/air-verse/air@latest
   ```

2. Run the Air server:
   ```bash
   air
   ```

3. The proxy will be available on port 8888, and the application will run on port 7777.

## Expected Behavior

Air's proxy should wait for the application to be ready before timing out.

## Actual Behavior

The proxy times out because the application takes 1 second to start (due to the `time.Sleep(1 * time.Second)` in `server.go`).

## Testing

Try accessing the server through the proxy:
```bash
curl http://localhost:7777
```
