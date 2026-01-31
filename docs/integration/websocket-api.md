# WebSocket API

Complete reference for Indigo's WebSocket API - real-time bidirectional communication for monitoring devices, variables, action groups, and logs.

## Quick Reference

| Feed | Endpoint | Purpose | Read | Write |
|------|----------|---------|------|-------|
| Device | `/v2/api/ws/device-feed` | Monitor/control devices | ✓ | ✓ |
| Variable | `/v2/api/ws/variable-feed` | Track variables | ✓ | ✓ |
| Action Group | `/v2/api/ws/action-feed` | Execute action groups | ✓ | ✓ |
| Control Page | `/v2/api/ws/page-feed` | Page management | ✓ | ✗ |
| Log | `/v2/api/ws/log-feed` | Real-time logging | ✓ | ✓ |

## Connection Lifecycle

### Phase 1: Connect

**Local Network**:
```python
import websockets
import json

uri = "ws://192.168.1.100:8176/v2/api/ws/device-feed"
headers = {'Authorization': f'Bearer {API_KEY}'}

async with websockets.connect(uri, extra_headers=headers) as ws:
    # Connected
```

**Remote (Reflector)**:
```python
uri = f"wss://{REFLECTOR}.indigodomo.net/v2/api/ws/device-feed"
```

### Phase 2: Request Initial Data

Send refresh message to get existing objects:

```python
await ws.send(json.dumps({
    "message": "refresh",
    "objectType": "indigo.Device"
}))

# Receive response with all devices
response = json.loads(await ws.recv())
# response["list"] contains array of all device objects
```

### Phase 3: Process Updates

Listen for add/patch/delete messages:

```python
async for message in ws:
    data = json.loads(message)

    if data["message"] == "add":
        # New device or device enabled for remote display
        device = data["objectDict"]

    elif data["message"] == "patch":
        # Device property changed
        device_id = data["objectId"]
        patch = data["patch"]  # dictdiffer format

    elif data["message"] == "delete":
        # Device removed or remote display disabled
        device_id = data["objectId"]
```

### Phase 4: Send Commands

```python
# Toggle device
await ws.send(json.dumps({
    "message": "indigo.device.toggle",
    "objectId": 123456789,
    "id": "optional-tracking-id"
}))
```

### Phase 5: Disconnect

```python
await ws.close()
```

## Message Types (Server → Client)

### Add Message

Sent when:
- New object created in Indigo
- Existing object's `remoteDisplay` set to `true`

```json
{
  "message": "add",
  "objectType": "indigo.Device",
  "objectDict": {
    "id": 123456789,
    "name": "Living Room Light",
    "class": "indigo.DimmerDevice",
    "brightness": 75,
    "onState": true,
    ...
  }
}
```

### Patch Message

Sent when object properties change. Uses [dictdiffer](https://github.com/inveniosoftware/dictdiffer) format:

```json
{
  "message": "patch",
  "objectType": "indigo.Device",
  "objectId": 123456789,
  "patch": [
    ["change", "brightness", [50, 75]],
    ["change", "onState", [false, true]]
  ]
}
```

**Patch Format**: `[operation, path, values]`
- `"change"` - Property modified: `[oldValue, newValue]`
- `"add"` - Property added: `[(key, value)]`
- `"remove"` - Property removed: `[(key, value)]`

### Delete Message

Sent when:
- Object deleted from Indigo
- Object's `remoteDisplay` set to `false`

```json
{
  "message": "delete",
  "objectType": "indigo.Device",
  "objectId": 123456789
}
```

### Refresh Response

Server reply to refresh requests:

```json
{
  "message": "refresh",
  "objectType": "indigo.Device",
  "list": [
    { "id": 123, "name": "Device 1", ... },
    { "id": 456, "name": "Device 2", ... }
  ],
  "id": "your-tracking-id"  // if you sent one
}
```

**Single object refresh**:
```json
{
  "message": "refresh",
  "objectType": "indigo.Device",
  "objectDict": { "id": 123456789, ... }
}
```

## Device Feed

### Refresh All Devices

```json
{
  "message": "refresh",
  "objectType": "indigo.Device"
}
```

### Refresh Single Device

```json
{
  "message": "refresh",
  "objectType": "indigo.Device",
  "objectId": 123456789
}
```

### Send Device Commands

See [device-commands.md](device-commands.md) for complete command reference.

```json
{
  "message": "indigo.device.toggle",
  "objectId": 123456789
}
```

```json
{
  "message": "indigo.dimmer.setBrightness",
  "objectId": 123456789,
  "parameters": {
    "value": 50,
    "delay": 0
  }
}
```

## Variable Feed

### Variable Object Structure

```json
{
  "class": "indigo.Variable",
  "id": 345633244,
  "name": "house_status",
  "value": "home",
  "readOnly": false,
  "description": "",
  "folderId": 0,
  "remoteDisplay": true,
  "globalProps": {},
  "pluginProps": {},
  "sharedProps": {}
}
```

### Update Variable Value

```json
{
  "message": "indigo.variable.updateValue",
  "objectId": 345633244,
  "parameters": {
    "value": "away"
  }
}
```

**Important**: Parameter values must be **strings**. Empty string `""` clears the value.

### Refresh Variables

```json
{
  "message": "refresh",
  "objectType": "indigo.Variable"
}
```

## Action Group Feed

### Action Group Object

```json
{
  "class": "indigo.ActionGroup",
  "id": 94914463,
  "name": "Movie Night",
  "description": "",
  "folderId": 532526508,
  "remoteDisplay": true,
  "globalProps": {},
  "pluginProps": {},
  "sharedProps": {}
}
```

### Execute Action Group

```json
{
  "message": "indigo.actionGroup.execute",
  "objectId": 94914463
}
```

### Refresh Action Groups

```json
{
  "message": "refresh",
  "objectType": "indigo.ActionGroup"
}
```

## Control Page Feed

**Read-only feed** - provides updates about control pages but does not accept commands.

Pages with `remoteDisplay: true` will generate add/patch/delete messages.

Use for building custom UI that mirrors Indigo's control pages.

## Log Feed

**Special behavior**:
- Upon connection, receives last **25 chronological messages**
- Then receives real-time log updates
- Only accepts `"add"` messages (read-only for logs)

### Send Log Message

```json
{
  "message": "indigo.server.log",
  "messageText": "Custom log entry from external app"
}
```

## Object Folders

### Refresh Folder List

```json
{
  "message": "refresh",
  "objectType": "indigo.Device.Folder"
}
```

Response:
```json
{
  "message": "refresh",
  "objectType": "indigo.Device.Folder",
  "list": [
    {"id": 123, "name": "Living Room", "remoteDisplay": true},
    {"id": 456, "name": "Bedroom", "remoteDisplay": true}
  ]
}
```

**Other folder types**:
- `"indigo.Variable.Folder"`
- `"indigo.ActionGroup.Folder"`

## Error Handling

### Generic Error Response

```json
{
  "error": "Error description",
  "errorId": "error-code"
}
```

### Connection Failures

**Causes**:
- Authentication failure
- Server not reachable
- Network timeout

**Best Practice**: Implement reconnection logic with exponential backoff

```python
import asyncio

async def connect_with_retry(uri, headers, max_retries=5):
    retry_delay = 1
    for attempt in range(max_retries):
        try:
            ws = await websockets.connect(uri, extra_headers=headers)
            return ws
        except Exception as e:
            if attempt < max_retries - 1:
                await asyncio.sleep(retry_delay)
                retry_delay *= 2  # Exponential backoff
            else:
                raise
```

## Complete Example (Python)

```python
import asyncio
import websockets
import json

API_KEY = "your_api_key"
REFLECTOR = "your_reflector"

async def monitor_devices():
    uri = f"wss://{REFLECTOR}.indigodomo.net/v2/api/ws/device-feed"
    headers = {'Authorization': f'Bearer {API_KEY}'}

    async with websockets.connect(uri, extra_headers=headers) as ws:
        # Request all devices
        await ws.send(json.dumps({
            "message": "refresh",
            "objectType": "indigo.Device"
        }))

        # Process messages
        async for message in ws:
            data = json.loads(message)

            if data["message"] == "refresh":
                devices = data.get("list", [])
                print(f"Received {len(devices)} devices")

            elif data["message"] == "add":
                device = data["objectDict"]
                print(f"Device added: {device['name']}")

            elif data["message"] == "patch":
                print(f"Device {data['objectId']} updated")
                for change in data["patch"]:
                    op, prop, values = change
                    if op == "change":
                        print(f"  {prop}: {values[0]} → {values[1]}")

            elif data["message"] == "delete":
                print(f"Device {data['objectId']} removed")

asyncio.run(monitor_devices())
```

## Complete Example (JavaScript/Node.js)

```javascript
const WebSocket = require('ws');

const API_KEY = 'your_api_key';
const REFLECTOR = 'your_reflector';

const ws = new WebSocket(`wss://${REFLECTOR}.indigodomo.net/v2/api/ws/device-feed`, {
  headers: { 'Authorization': `Bearer ${API_KEY}` }
});

ws.on('open', function() {
  // Request all devices
  ws.send(JSON.stringify({
    message: 'refresh',
    objectType: 'indigo.Device'
  }));
});

ws.on('message', function(data) {
  const msg = JSON.parse(data);

  if (msg.message === 'refresh') {
    console.log(`Received ${msg.list.length} devices`);
  } else if (msg.message === 'add') {
    console.log(`Device added: ${msg.objectDict.name}`);
  } else if (msg.message === 'patch') {
    console.log(`Device ${msg.objectId} updated`);
  } else if (msg.message === 'delete') {
    console.log(`Device ${msg.objectId} removed`);
  }
});

ws.on('error', function(error) {
  console.error('WebSocket error:', error);
});
```

## Best Practices

1. **Connection Management**: Implement automatic reconnection with exponential backoff
2. **Message Tracking**: Use optional `id` field to track request/response pairs
3. **Patch Handling**: Use dictdiffer library to apply patches efficiently
4. **Error Logging**: Log all errors with context for debugging
5. **Resource Cleanup**: Always close WebSocket connections properly
6. **Rate Limiting**: Don't send commands faster than devices can process
7. **Object Caching**: Maintain local copy of objects, apply patches incrementally

## Related Documentation

- **[Device Commands](device-commands.md)** - All available device commands
- **[HTTP API](http-api.md)** - Alternative REST API
- **[Authentication](authentication.md)** - Setup and security
- **[Overview](overview.md)** - When to use WebSocket vs HTTP
