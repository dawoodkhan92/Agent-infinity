# Agent Infinity

A WhatsApp customer-support bot that turns a folder of AI agent tools into live HTTP endpoints — drop in a tool, get an API.

Built with **Flask + Twilio + [Agency Swarm](https://github.com/VRSEN/agency-swarm)**. Designed to deploy in minutes on Railway.

## How it works

Every Python file you put in `./tools/` is auto-discovered at startup and exposed as its own authenticated `POST` endpoint — no manual route wiring. Incoming WhatsApp messages (via Twilio) are routed to the right agent tool, which runs and replies.

```
WhatsApp message ──▶ Twilio ──▶ Flask endpoint ──▶ Agent tool ──▶ reply
```

## Quick start

```bash
git clone https://github.com/dawoodkhan92/Agent-infinity.git
cd Agent-infinity
pip install -r requirements.txt
cp .env.example .env      # add your Twilio + DB_TOKEN secrets
python main.py
```

Endpoints are protected with a bearer token (`DB_TOKEN`) — every request must send `Authorization: Bearer <token>`.

## Adding a tool

1. Create a new `.py` file in `./tools/` defining an Agency Swarm tool class.
2. Restart — it's automatically registered as `POST /<ToolName>`.

## Deploy

Ships with `railway.json` and a config for one-click [Railway](https://railway.app) deployment.

## Stack

Python · Flask · Gunicorn · Twilio · Agency Swarm

## License

MIT
