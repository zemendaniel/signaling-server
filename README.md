# Signaling Server

A simple **FastAPI WebSocket server** to help peers exchange information in the [ZettaSend](https://zettasend.com) and [zemendaniel/QuicShare](https://github.com/zemendaniel/QuicShare) project.
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

## Environment Variables

Create your local env file from the example:

```bash
cp .env.example .env
```

The server loads variables from `.env` at startup.
All the variables are optional, however if you want to use the relay fallback, you need to set the relay variables.

| Variable                       | Default                     | Description                                                      |
|--------------------------------|-----------------------------|------------------------------------------------------------------|
| `LOG_LEVEL`                    | `INFO`                      | Python logging level for console and file logging.               |
| `LOG_FILE`                     | `logs/signaling-server.log` | Log output file path. Parent directory is created automatically. |
| `REDIS_HOST`                   | `localhost`                 | Redis host used by the signaling server.                         |
| `REDIS_PORT`                   | `6379`                      | Redis port used by the signaling server.                         |
| `ROOM_EXPIRE`                  | `300`                       | Room/session inactivity timeout in seconds.                      |
| `MAX_MESSAGE_SIZE`             | `4096`                      | Maximum allowed WebSocket message size in bytes.                 |
| `MAX_ROOM_GENERATION_ATTEMPTS` | `1000`                      | Max attempts to generate a unique room id.                       |
| `RELAY_URL_BASE`               | *(unset)*                   | Base URL for optional relay allocation API.                      |
| `RELAY_PUBLIC_HOST`            | *(unset)*                   | Public relay hostname shared with peers.                         |
| `RELAY_KEY`                    | *(unset)*                   | API key sent as `x-relay-api-key` for relay allocation.          |

## Notes

* Make sure your firewall allows traffic to the server.
* This server doesn’t encrypt traffic by default. For secure connections, use a reverse proxy with SSL.
* I built this mainly for simple peer discovery between 2 peers, but you’re welcome to fork it and adapt it for your own projects. If you find it useful, a star on the repo would be awesome!
