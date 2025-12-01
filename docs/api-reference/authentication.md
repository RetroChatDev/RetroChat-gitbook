# Authentication

Learn how to authenticate API requests to RetroChat.

## API Keys

### Getting an API Key
1. Log in to RetroChat
2. Go to Settings → API
3. Generate new API key
4. Copy and store securely
5. Use in API requests

### API Key Format
- Format: `rc_xxxxxxxxxxxxxxxx`
- Keep secret
- Don't share publicly
- Rotate regularly

## Authentication Methods

### Header Authentication
Include API key in request headers:

```
Authorization: Bearer YOUR_API_KEY
```

### Query Parameter (Not Recommended)
For testing only:
```
?api_key=YOUR_API_KEY
```

## Request Example

```bash
curl -X GET \
  https://api.retrochat.io/v1/users/me \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## Scopes & Permissions

### API Scopes
- Read access
- Write access
- Admin access
- Web3 access

### Permission Levels
- User: Basic access
- Moderator: Enhanced access
- Admin: Full access

## Security Best Practices

1. **Store Securely**: Never commit keys to code
2. **Use Environment Variables**: Keep keys in env files
3. **Rotate Regularly**: Change keys periodically
4. **Limit Scope**: Use minimum required permissions
5. **Monitor Usage**: Watch for unauthorized access

## Token Refresh

### Access Tokens
- Short-lived tokens
- Refresh mechanism
- Automatic refresh
- Manual refresh option

### Refresh Tokens
- Long-lived tokens
- Secure storage
- Rotation support
- Revocation

## Error Handling

### Authentication Errors
- 401 Unauthorized
- 403 Forbidden
- Token expired
- Invalid credentials

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "AUTH_ERROR",
    "message": "Authentication failed"
  }
}
```

## WebSocket Authentication

### Connection Authentication
- Include token in connection
- Token validation
- Secure connection
- Session management

## Resources

- [REST Endpoints](./rest-endpoints.md)
- [Realtime Subscriptions](./realtime-subscriptions.md)
- [Edge Functions](./edge-functions.md)

