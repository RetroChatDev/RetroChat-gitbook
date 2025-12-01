# REST Endpoints

Complete reference for RetroChat REST API endpoints.

## Base URL

```
https://api.retrochat.io/v1
```

## Endpoints

### Users

#### Get Current User
```
GET /users/me
```

#### Get User
```
GET /users/{userId}
```

#### Update User
```
PATCH /users/me
```

### Messages

#### Get Messages
```
GET /messages
```

#### Send Message
```
POST /messages
```

#### Delete Message
```
DELETE /messages/{messageId}
```

### Rooms

#### List Rooms
```
GET /rooms
```

#### Get Room
```
GET /rooms/{roomId}
```

#### Create Room
```
POST /rooms
```

#### Update Room
```
PATCH /rooms/{roomId}
```

#### Delete Room
```
DELETE /rooms/{roomId}
```

### Direct Messages

#### Get Conversations
```
GET /conversations
```

#### Get Messages
```
GET /conversations/{conversationId}/messages
```

#### Send Message
```
POST /conversations/{conversationId}/messages
```

### Web3

#### Get Wallet
```
GET /wallet
```

#### Connect Wallet
```
POST /wallet/connect
```

#### Send Tip
```
POST /tips
```

#### Get Airdrops
```
GET /airdrops
```

## Request/Response Examples

### Get Current User
**Request:**
```bash
GET /users/me
Authorization: Bearer YOUR_API_KEY
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "user_123",
    "username": "example",
    "email": "user@example.com",
    "avatar": "https://...",
    "created_at": "2025-01-01T00:00:00Z"
  }
}
```

### Send Message
**Request:**
```bash
POST /messages
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json

{
  "room_id": "room_123",
  "content": "Hello, world!",
  "type": "text"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": "msg_123",
    "room_id": "room_123",
    "user_id": "user_123",
    "content": "Hello, world!",
    "created_at": "2025-01-01T00:00:00Z"
  }
}
```

## Error Codes

- `400` Bad Request
- `401` Unauthorized
- `403` Forbidden
- `404` Not Found
- `429` Rate Limited
- `500` Server Error

## Rate Limits

- Standard: 100 requests/minute
- Burst: 200 requests/minute
- Headers indicate limits
- Upgrade available

## Pagination

### Paginated Endpoints
- Use `page` and `limit` parameters
- Response includes pagination metadata

### Example
```
GET /messages?page=1&limit=50
```

## Filtering & Sorting

### Filtering
- Filter by various fields
- Multiple filters supported
- Query parameter format

### Sorting
- Sort by field
- Ascending/descending
- Multiple sort fields

## Resources

- [Authentication](./authentication.md)
- [Realtime Subscriptions](./realtime-subscriptions.md)
- [Edge Functions](./edge-functions.md)

