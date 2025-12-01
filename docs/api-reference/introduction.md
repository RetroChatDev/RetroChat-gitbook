# API Reference - Introduction

Welcome to the RetroChat API reference documentation.

## Overview

The RetroChat API allows developers to integrate RetroChat functionality into their applications and build custom solutions.

## API Versions

### Current Version
- API Version: v1
- Base URL: `https://api.retrochat.io/v1`
- Status: Stable

### Versioning
- Version in URL path
- Backward compatibility
- Deprecation notices
- Migration guides

## Getting Started

### Prerequisites
- RetroChat account
- API key (for authenticated endpoints)
- Basic HTTP knowledge
- JSON understanding

### Quick Start
1. [Get your API key](./authentication.md)
2. Make your first request
3. Explore endpoints
4. Build your integration

## API Features

### REST API
- Standard HTTP methods
- JSON responses
- Error handling
- Rate limiting

### Realtime API
- WebSocket connections
- Real-time updates
- Event subscriptions
- Live data

### Edge Functions
- Serverless functions
- Custom logic
- Integration hooks
- Event handlers

## Authentication

All API requests require authentication. See [Authentication](./authentication.md) for details.

## Rate Limits

- Rate limits apply to all endpoints
- Limits vary by endpoint
- Headers indicate limits
- Upgrade options available

## Response Format

### Success Response
```json
{
  "success": true,
  "data": { ... },
  "meta": { ... }
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Error message"
  }
}
```

## Resources

- [Authentication](./authentication.md)
- [REST Endpoints](./rest-endpoints.md)
- [Realtime Subscriptions](./realtime-subscriptions.md)
- [Edge Functions](./edge-functions.md)

