# Indigo Integration APIs Skill

Claude Code skill for building applications that integrate with [Indigo](https://www.indigodomo.com) home automation via WebSocket and HTTP APIs.

## What is This?

This skill provides expert assistance for **client-side development** - building iOS/Android apps, web dashboards, and third-party integrations that connect TO Indigo.

**Not what you're looking for?**
- For **server-side plugin development** (building Indigo plugins in Python), use the [Indigo Plugin Development Skill](https://github.com/simons-plugins/indigo-claude-skill) instead.

## What's Included

### 📡 Complete API Documentation
- **WebSocket API** - Real-time bidirectional communication
- **HTTP/REST API** - Stateless request/response endpoints
- **Authentication** - API keys, OAuth, security best practices
- **Device Commands** - Complete reference for all device types

### 💻 Code Examples
- Python (requests, websockets)
- JavaScript/Node.js (fetch, ws)
- curl (command-line examples)

### 🎯 Use Cases Covered
- iOS/Android mobile apps
- Web dashboards and control interfaces
- Automation scripts
- Third-party service integrations
- Real-time monitoring
- Remote device control

## Installation

### Option 1: Clone into Project

```bash
cd /path/to/your/project
mkdir -p .claude/skills
git clone https://github.com/simons-plugins/indigo-api-skill.git .claude/skills/indigo-api
```

### Option 2: Add as Submodule

```bash
cd /path/to/your/project
mkdir -p .claude/skills
git submodule add https://github.com/simons-plugins/indigo-api-skill.git .claude/skills/indigo-api
```

### Option 3: Symlink (for Multiple Projects)

```bash
# Clone once
git clone https://github.com/simons-plugins/indigo-api-skill.git ~/indigo-api-skill

# Symlink in each project
cd /path/to/your/project
mkdir -p .claude/skills
ln -s ~/indigo-api-skill .claude/skills/indigo-api
```

## Usage

Invoke the skill in Claude Code:

```
/indigo-api "How do I build an iOS app that monitors Indigo devices?"
/indigo-api "Show me WebSocket API example for device monitoring"
/indigo-api "What's the HTTP endpoint to control a dimmer?"
/indigo-api "How do I setup API authentication?"
```

## Quick Examples

### Get Started

```
/indigo-api "I want to build a web dashboard for Indigo"
/indigo-api "Should I use WebSocket or HTTP for my app?"
/indigo-api "Show me authentication setup"
```

### WebSocket API

```
/indigo-api "Connect to WebSocket device feed"
/indigo-api "Monitor device changes in real-time"
/indigo-api "What WebSocket feeds are available?"
```

### HTTP API

```
/indigo-api "Get all devices via HTTP"
/indigo-api "Turn on a light with curl"
/indigo-api "Show me Python requests example"
```

### Device Commands

```
/indigo-api "How do I set dimmer brightness?"
/indigo-api "What commands work with thermostats?"
/indigo-api "Show me all device command messages"
```

## Documentation Structure

```
docs/integration/
├── README.md              # Quick navigation
├── overview.md            # WebSocket vs HTTP decision guide
├── authentication.md      # API keys and security
├── websocket-api.md      # WebSocket API complete reference
├── http-api.md           # HTTP/REST API complete reference
└── device-commands.md    # All device command messages
```

## What You Can Build

### Mobile Apps
Build native iOS/Android apps with real-time device monitoring:
- Live device status updates via WebSocket
- Control devices with instant feedback
- Push notifications for device changes
- Offline support with HTTP fallback

### Web Dashboards
Create custom web interfaces for Indigo:
- Real-time status displays
- Interactive device control
- Custom visualizations
- Multi-user access

### Automation Scripts
Automate Indigo with external scripts:
- Python/Node.js automation
- cron job integrations
- Shell scripts with curl
- CI/CD pipeline triggers

### Third-Party Integrations
Connect Indigo to other services:
- Home Assistant bridges
- Google Home/Alexa custom skills
- IFTTT/Zapier webhooks
- Monitoring/analytics platforms

## API Overview

### WebSocket API
**Best for**: Real-time monitoring, mobile apps, live dashboards

- Persistent bidirectional connection
- 5 specialized feeds (devices, variables, actions, pages, logs)
- Automatic push notifications when state changes
- Efficient for continuous monitoring

### HTTP API
**Best for**: Scripts, periodic checks, webhooks

- Stateless request/response model
- Standard GET/POST endpoints
- Works with any HTTP library (curl, requests, fetch)
- Perfect for occasional access

### Same Commands, Two Transports
Both APIs use identical command messages - choose the transport that fits your use case.

## Authentication

Both APIs support:
- **API Keys** (recommended) - Per-app, revocable, secure
- **Local Secrets** - Shared secret for trusted local network

API keys created at [Indigo Account Portal](https://www.indigodomo.com/account/).

## Requirements

- Indigo 2025.1 or later
- "Start Local Server" enabled in Indigo preferences
- API authentication enabled (OAuth/API Keys)
- Network access to Indigo server (local or via Reflector)

## Related Skills

### Indigo Plugin Development Skill
For **server-side plugin development** (building Indigo plugins in Python):
→ [indigo-claude-skill](https://github.com/simons-plugins/indigo-claude-skill)
→ Use `/indigo` command

### This Skill
For **client-side integration** (building apps that connect to Indigo):
→ This repository
→ Use `/indigo-api` command

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### What to Contribute
- 📝 Documentation improvements
- 💻 Code examples in additional languages
- 📚 Additional use case guides
- 🐛 Bug reports and corrections

## Community

- 💬 **Discussions**: Ask questions, share tips
- 🐛 **Issues**: Report bugs or request features
- 🌐 **Forum**: [Indigo Developer Forum](https://forums.indigodomo.com/)

## Official Resources

- [Indigo API Documentation](https://wiki.indigodomo.com/doku.php?id=indigo_2025.1_documentation:api)
- [Indigo Website](https://www.indigodomo.com)
- [Indigo Forum](https://forums.indigodomo.com/)

## License

MIT License - See [LICENSE](LICENSE)

## Maintainers

This is a community project. Want to help maintain? Open an issue or discussion!

---

**Made with ❤️ by the Indigo developer community**

**For client-side integration** | Use `/indigo` skill for server-side plugin development
