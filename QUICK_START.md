# Quick Start Guide

Get started with Indigo Integration APIs in 5 minutes!

## Installation

```bash
cd /path/to/your/project
mkdir -p .claude/skills
git clone https://github.com/simons-plugins/indigo-api-skill.git .claude/skills/indigo-api
```

## Verify Installation

In Claude Code, try:

```
/indigo-api "Hello! Are you working?"
```

If installed correctly, Claude will respond with Indigo API knowledge.

## Basic Usage

### Getting Started

```
/indigo-api "I want to build an iOS app that monitors Indigo devices"
/indigo-api "Should I use WebSocket or HTTP?"
/indigo-api "Show me authentication setup"
```

### WebSocket API

```
/indigo-api "How do I connect to WebSocket device feed?"
/indigo-api "Show me real-time device monitoring example"
/indigo-api "What WebSocket feeds are available?"
```

### HTTP API

```
/indigo-api "How do I get all devices via HTTP?"
/indigo-api "Show me curl example to turn on a light"
/indigo-api "What's the endpoint for controlling devices?"
```

### Device Commands

```
/indigo-api "How do I set dimmer brightness?"
/indigo-api "What commands work with thermostats?"
/indigo-api "Show me all device control commands"
```

### Authentication

```
/indigo-api "How do I setup API keys?"
/indigo-api "What's the difference between API keys and local secrets?"
/indigo-api "How do I secure my API connection?"
```

## Example Interactions

### Building an iOS App

**You**: `/indigo-api "I want to build an iOS app that shows my Indigo devices with real-time updates"`

**Claude**: Will provide:
- Recommendation to use WebSocket API for real-time
- API key setup instructions
- Swift/iOS WebSocket connection example
- Device monitoring pattern
- Command sending examples

### Creating a Web Dashboard

**You**: `/indigo-api "Create a web dashboard to control my lights"`

**Claude**: Will help with:
- HTTP GET for initial device list
- WebSocket for real-time updates
- JavaScript fetch() and WebSocket examples
- Authentication setup
- Control command implementation

### Writing an Automation Script

**You**: `/indigo-api "I want a Python script to turn off all lights at midnight"`

**Claude**: Will provide:
- Python requests library examples
- HTTP POST command endpoint usage
- Authentication with API keys
- Device command syntax
- Error handling

## What the Skill Knows

The skill has access to:

### ✅ API Documentation
- WebSocket API complete reference
- HTTP/REST API endpoints
- Authentication and security
- All device command messages

### ✅ Code Examples
- Python (requests, websockets)
- JavaScript (fetch, WebSocket)
- curl command-line examples
- Real-world integration patterns

### ✅ Best Practices
- WebSocket vs HTTP decision guide
- Connection management
- Error handling
- Security recommendations
- Performance optimization

## Tips for Best Results

### Be Specific

❌ "Help with Indigo API"
✅ "Show me WebSocket code to monitor temperature sensors in Python"

### Provide Context

```
/indigo-api "I'm building an iOS app in Swift. I need to monitor devices in real-time and send commands. What's the best approach?"
```

### Ask Follow-up Questions

```
/indigo-api "Can you show the WebSocket connection code in JavaScript?"
/indigo-api "How do I handle reconnection if the connection drops?"
/indigo-api "What if the API returns an error?"
```

## Common Use Cases

### 1. iOS/Android App

```
/indigo-api "Build iOS app for Indigo device monitoring and control"
```

### 2. Web Dashboard

```
/indigo-api "Create real-time web dashboard with JavaScript"
```

### 3. Automation Script

```
/indigo-api "Python script to control lights via HTTP API"
```

### 4. Third-Party Integration

```
/indigo-api "Integrate Indigo with Home Assistant using webhooks"
```

## Documentation Overview

```
docs/integration/
├── README.md              # Quick navigation
├── overview.md            # WebSocket vs HTTP decision guide
├── authentication.md      # API keys and security
├── websocket-api.md      # WebSocket API reference
├── http-api.md           # HTTP/REST API reference
└── device-commands.md    # All device commands
```

## Related Skills

### For Plugin Development
If you're building **Indigo plugins** (server-side Python):
→ Use `/indigo` skill instead
→ [indigo-claude-skill](https://github.com/simons-plugins/indigo-claude-skill)

### For API Integration
If you're building **apps that connect to Indigo** (client-side):
→ Use `/indigo-api` skill (this one!)

## Next Steps

1. **Setup authentication**: `/indigo-api "How do I setup API authentication?"`
2. **Choose your API**: `/indigo-api "Should I use WebSocket or HTTP?"`
3. **Start coding**: `/indigo-api "Show me [Python/JavaScript/Swift] example for [use case]"`

## Need More Help?

- 📚 Read the [README](README.md)
- 💬 Join [Discussions](https://github.com/simons-plugins/indigo-api-skill/discussions)
- 🐛 Report [Issues](https://github.com/simons-plugins/indigo-api-skill/issues)
- 🌐 Visit [Indigo Forum](https://forums.indigodomo.com/)

---

Happy integrating! 🚀
