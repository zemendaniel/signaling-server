# Signaling Server

A simple **FastAPI WebSocket server** to help peers exchange information in the [zemendaniel/QuicShare](https://github.com/zemendaniel/QuicShare) project.
It uses **Redis** for message passing.

## Features

* Quick and easy peer-to-peer signaling with WebSockets
* Redis backend for smooth message routing
* Simple setup using Docker
* Optional scaling with Docker Compose if you need more instances

## Installation

```bash
git clone https://github.com/zemendaniel/signaling-server.git
cd signaling-server
docker buildx build .
docker compose up -d --scale fastapi=3
```

## Usage

Once the server is up, you can reach it on **port 8080**. You can check the /health endpoint for health status.

## Notes

* Make sure your firewall allows traffic to the server.
* This server doesn’t encrypt traffic by default. For secure connections, use a reverse proxy with SSL.
* I built this mainly for simple peer discovery between 2 peers, but you’re welcome to fork it and adapt it for your own projects. If you find it useful, a star on the repo would be awesome!
