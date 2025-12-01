# Realtime Subscriptions

Subscribe to real-time events using RetroChat's WebSocket API.

## WebSocket Connection

### Connection URL
```
wss://api.retrochat.io/v1/realtime
```

### Authentication
Include authentication token in connection:
```
Authorization: Bearer YOUR_API_KEY
```

## Connection Example

```javascript
const ws = new WebSocket('wss://api.retrochat.io/v1/realtime', {
  headers: {
    'Authorization': 'Bearer YOUR_API_KEY'
  }
});

ws.on('open', () => {
  console.log('Connected');
});

ws.on('message', (data) => {
  const event = JSON.parse(data);
  console.log('Event:', event);
});
```

## Subscription Types

### Room Messages
Subscribe to messages in a room:
```json
{
  "type": "subscribe",
  "channel": "room:123",
  "event": "message"
}
```

### Direct Messages
Subscribe to direct messages:
```json
{
  "type": "subscribe",
  "channel": "conversation:123",
  "event": "message"
}
```

### User Activity
Subscribe to user activity:
```json
{
  "type": "subscribe",
  "channel": "user:123",
  "event": "activity"
}
```

## Event Types

### Message Events
- `message:new` - New message
- `message:updated` - Message updated
- `message:deleted` - Message deleted

### User Events
- `user:online` - User came online
- `user:offline` - User went offline
- `user:updated` - User profile updated

### Room Events
- `room:created` - Room created
- `room:updated` - Room updated
- `room:deleted` - Room deleted

## Event Payloads

### Message Event
```json
{
  "type": "message:new",
  "channel": "room:123",
  "data": {
    "id": "msg_123",
    "room_id": "room_123",
    "user_id": "user_123",
    "content": "Hello!",
    "created_at": "2025-01-01T00:00:00Z"
  }
}
```

### User Event
```json
{
  "type": "user:online",
  "channel": "user:123",
  "data": {
    "user_id": "user_123",
    "status": "online",
    "timestamp": "2025-01-01T00:00:00Z"
  }
}
```

## Subscription Management

### Subscribe
```json
{
  "type": "subscribe",
  "channel": "room:123",
  "event": "message"
}
```

### Unsubscribe
```json
{
  "type": "unsubscribe",
  "channel": "room:123"
}
```

### List Subscriptions
```json
{
  "type": "list_subscriptions"
}
```

## Error Handling

### Connection Errors
- Handle disconnections
- Reconnect logic
- Error events
- Status monitoring

### Error Events
```json
{
  "type": "error",
  "code": "ERROR_CODE",
  "message": "Error message"
}
```

## Best Practices

1. **Reconnect Logic**: Handle disconnections
2. **Rate Limiting**: Don't overwhelm server
3. **Error Handling**: Handle errors gracefully
4. **Cleanup**: Unsubscribe when done
5. **Security**: Keep tokens secure

## Resources

- [Authentication](./authentication.md)
- [REST Endpoints](./rest-endpoints.md)
- [Edge Functions](./edge-functions.md)

