# Indigo Integration APIs Expert

**Repository**: https://github.com/simons-plugins/indigo-api-skill
**Version**: 2025.1
**Slash command**: `/indigo-api`

## Description

Expert assistant for building applications that integrate with Indigo home automation via WebSocket and HTTP APIs. Perfect for iOS/Android apps, web dashboards, and third-party service integrations.

**Note**: This skill is for **client-side development** (apps that connect TO Indigo). For **server-side plugin development** (building Indigo plugins), use the `/indigo` skill instead.

## CRITICAL: Context Optimization Strategy

This skill contains focused API documentation (~50KB). Load selectively based on query type.

### All Files (Load by Topic)

| File | Size | Use For |
|------|------|---------|
| `docs/integration/README.md` | 5KB | Navigation and quick lookup |
| `docs/integration/overview.md` | 7KB | WebSocket vs HTTP decision |
| `docs/integration/authentication.md` | 7KB | API key setup and security |
| `docs/integration/websocket-api.md` | 10KB | WebSocket API reference |
| `docs/integration/http-api.md` | 11KB | HTTP/REST API reference |
| `docs/integration/device-commands.md` | 12KB | Complete command reference |

**Total**: ~52KB across 6 files - load selectively.

## Query Routing Guide

### General Integration Questions

**"Build iOS/web app" / "Get started with Indigo API"**
1. Read `docs/integration/overview.md` (WebSocket vs HTTP decision)
2. Read `docs/integration/authentication.md` (API key setup)

**"Should I use WebSocket or HTTP?"**
1. Read `docs/integration/overview.md`

### WebSocket API Questions

**"Monitor devices in real-time" / "WebSocket API" / "Live updates"**
1. Read `docs/integration/websocket-api.md`
2. If auth needed: Read `docs/integration/authentication.md`

**Examples:**
- "How do I connect to WebSocket feed?"
- "Show me WebSocket example for device monitoring"
- "What WebSocket feeds are available?"
- "How do I subscribe to device changes?"

### HTTP API Questions

**"Control via REST API" / "HTTP endpoints" / "curl examples"**
1. Read `docs/integration/http-api.md`
2. If auth needed: Read `docs/integration/authentication.md`

**Examples:**
- "What's the HTTP endpoint to get all devices?"
- "Show me curl example for turning on a light"
- "How do I control a dimmer via REST API?"
- "Get single device via HTTP"

### Command Reference Questions

**"What commands can I send?" / "Device commands" / "Control devices"**
1. Read `docs/integration/device-commands.md`

**Examples:**
- "How do I turn on a device?"
- "What commands work with dimmers?"
- "Show me all device command messages"
- "How do I set brightness?"
- "What parameters does toggle command take?"

### Authentication Questions

**"Setup API keys" / "Authentication" / "Security"**
1. Read `docs/integration/authentication.md`

**Examples:**
- "How do I setup API authentication?"
- "Where do I get API keys?"
- "How do I secure my API connection?"
- "What's the difference between API keys and local secrets?"

## Workflow Examples

### Building an iOS App

**User**: "I want to build an iOS app that shows my Indigo devices in real-time"

**Assistant**:
1. Read `docs/integration/overview.md` → Explain WebSocket is best for real-time
2. Read `docs/integration/authentication.md` → Show API key setup
3. Read `docs/integration/websocket-api.md` → Provide connection example
4. Read `docs/integration/device-commands.md` → Show control commands

### Building a Web Dashboard

**User**: "Create a web dashboard to control my lights"

**Assistant**:
1. Read `docs/integration/overview.md` → Suggest HTTP for initial load, WebSocket for updates
2. Read `docs/integration/authentication.md` → API key setup
3. Read `docs/integration/http-api.md` → Show GET /devices endpoint
4. Read `docs/integration/websocket-api.md` → Real-time updates
5. Read `docs/integration/device-commands.md` → Control commands

### Simple Automation Script

**User**: "I want to turn off all lights via curl script"

**Assistant**:
1. Read `docs/integration/http-api.md` → Show curl examples
2. Read `docs/integration/authentication.md` → Header authentication
3. Read `docs/integration/device-commands.md` → turnOff command

## Key Concepts

### Two APIs Available

1. **WebSocket API** - Real-time, bidirectional, persistent connection
   - Best for: Mobile apps, live dashboards, continuous monitoring
   - Use when: Need instant updates when devices change

2. **HTTP API** - Stateless, request/response, standard REST
   - Best for: Scripts, webhooks, periodic checks
   - Use when: Occasional commands or polling is acceptable

### Same Commands, Two Transports

Both APIs use the **same command messages** (documented in `device-commands.md`):
- WebSocket sends commands via persistent connection
- HTTP sends commands via POST to `/v2/api/command`

### Authentication

Both APIs use **API Keys** or **Local Secrets**:
- API Keys: Created in Indigo Account portal, per-app, revocable
- Local Secrets: Shared secret in Indigo preferences, local network only

## Common Use Cases

### iOS/Android App
→ WebSocket API for real-time device status
→ Send commands via WebSocket
→ Files: `websocket-api.md`, `authentication.md`, `device-commands.md`

### Web Dashboard
→ HTTP for initial page load
→ WebSocket for live updates
→ Files: `http-api.md`, `websocket-api.md`, `device-commands.md`

### Automation Script
→ HTTP API with curl/requests
→ Simple polling or command execution
→ Files: `http-api.md`, `device-commands.md`

### Third-Party Integration
→ Webhooks receive HTTP POST
→ WebSocket for monitoring Indigo events
→ Files: `http-api.md`, `websocket-api.md`

## Related Skills

**Building Indigo Plugins** (server-side Python development):
→ Use `/indigo` skill for plugin development

**This Skill** (client-side integration):
→ Use `/indigo-api` for building apps that connect to Indigo

## External Resources

- [Official API Documentation](https://wiki.indigodomo.com/doku.php?id=indigo_2025.1_documentation:api)
- [Indigo Forum](https://forums.indigodomo.com/)
- [Indigo Account Portal](https://accounts.indigodomo.com) - Create API keys

## Version Information

- **Current**: Indigo 2025.1+ API
- **Protocol**: WebSocket (WSS/WS), HTTP (HTTPS/HTTP)
- **Authentication**: API Keys (recommended), Local Secrets
