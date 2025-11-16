# Deploy Caddy - Reverse Proxy Configuration

This repository configures Caddy as a reverse proxy for `hollant.dashlab.in:443` with automatic HTTPS using Cloudflare DNS-01 challenge.

## Features

- Reverse proxy to `hollant.dashlab.in:443`
- Automatic HTTPS certificate management via Let's Encrypt
- DNS-01 challenge using Cloudflare DNS
- HTTP/3 support (QUIC)
- Automatic HTTP to HTTPS redirect

## Prerequisites

- Docker and Docker Compose
- Cloudflare account with API token
- DNS records managed by Cloudflare for `hollant.dashlab.in`

## Setup

1. Clone this repository

2. Create a `.env` file from the example:
   ```bash
   cp .env.example .env
   ```

3. Edit `.env` and add your Cloudflare API token:
   ```
   CLOUDFLARE_API_TOKEN=your_actual_token_here
   ```

   To create a Cloudflare API token:
   - Go to Cloudflare Dashboard → My Profile → API Tokens
   - Create a token with `Zone:DNS:Edit` permissions for your domain
   - Copy the token to your `.env` file

4. Build and start the container:
   ```bash
   docker compose up -d --build
   ```

5. Check logs:
   ```bash
   docker compose logs -f
   ```

## Configuration

- **Caddyfile**: Contains the Caddy server configuration
- **docker-compose.yml**: Defines the Docker service and volumes
- **Dockerfile**: Builds Caddy with the Cloudflare DNS plugin

## Volumes

- `caddy_data`: Stores certificates and other data
- `caddy_config`: Stores Caddy's configuration cache

## Ports

- `80`: HTTP (automatically redirects to HTTPS)
- `443/tcp`: HTTPS
- `443/udp`: HTTP/3 (QUIC)

## Stopping

```bash
docker compose down
```

To remove volumes as well:
```bash
docker compose down -v
```
