# Rate Limiting

<div align="center">

# ⚡ Rate Limiting
### Control and Optimize API Access

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/rate-limiting)
[![Use Case](https://img.shields.io/badge/Use%20Case-Performance-blue?style=for-the-badge)](https://docs.mockgee.com/features/rate-limiting)

</div>

## Overview

Rate limiting in Mockgee helps you control API access, prevent abuse, and ensure optimal performance. Configure limits based on various criteria like IP, tokens, or custom rules.

## Key Features

### 🎯 Limiting Strategies
- Request-based limits
- Window-based throttling
- Token bucket algorithm
- Custom rate rules

### 🔄 Limit Types
- Global limits
- Per-endpoint limits
- Per-client limits
- Custom criteria

## Implementation Guide

### 1. Basic Rate Limiting

```javascript
{
  "rateLimiting": {
    "enabled": true,
    "global": {
      "requests": 1000,
      "window": "1h"
    }
  }
}
```

### 2. Per-Endpoint Configuration

```javascript
{
  "endpoint": "/api/resources",
  "rateLimiting": {
    "get": {
      "requests": 100,
      "window": "1m"
    },
    "post": {
      "requests": 50,
      "window": "1m"
    }
  }
}
```

### 3. Advanced Configuration

```javascript
{
  "rateLimiting": {
    "rules": [
      {
        "matcher": {
          "path": "/api/premium/*",
          "method": "POST"
        },
        "limit": {
          "requests": 200,
          "window": "1h",
          "scope": "ip"
        }
      },
      {
        "matcher": {
          "headers": {
            "API-Key": "*"
          }
        },
        "limit": {
          "requests": 1000,
          "window": "1d",
          "scope": "api-key"
        }
      }
    ]
  }
}
```

## Advanced Features

### 1. 🎯 Dynamic Rate Limiting

```javascript
{
  "rateLimiting": {
    "dynamic": {
      "enabled": true,
      "factors": {
        "serverLoad": {
          "threshold": 80,
          "reduction": 0.5
        },
        "errorRate": {
          "threshold": 0.05,
          "reduction": 0.7
        }
      }
    }
  }
}
```

### 2. 🔄 Token Bucket Implementation

```javascript
{
  "rateLimiting": {
    "tokenBucket": {
      "capacity": 100,
      "refillRate": 10,
      "refillInterval": "1s",
      "initialTokens": 100
    }
  }
}
```

### 3. 📊 Custom Rate Rules

```javascript
{
  "rateLimiting": {
    "custom": {
      "rules": [
        {
          "condition": "request.headers['User-Type'] === 'premium'",
          "limit": {
            "requests": 5000,
            "window": "1h"
          }
        },
        {
          "condition": "request.query.priority === 'high'",
          "limit": {
            "requests": 2000,
            "window": "1h"
          }
        }
      ]
    }
  }
}
```

## Headers and Responses

### Rate Limit Headers

```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1635789600
```

### Rate Limit Response

```javascript
// When limit exceeded
{
  "status": 429,
  "error": "Too Many Requests",
  "message": "Rate limit exceeded. Please try again in 60 seconds",
  "details": {
    "limitType": "ip",
    "currentUsage": 100,
    "limit": 100,
    "resetAt": "2024-02-05T12:00:00Z"
  }
}
```

## Best Practices

### 1. Configuration Strategy
- Start with conservative limits
- Monitor usage patterns
- Adjust based on metrics
- Consider user tiers

### 2. Implementation Tips
- Use appropriate window sizes
- Set reasonable limits
- Include buffer capacity
- Implement graceful degradation

### 3. Error Handling
- Clear error messages
- Retry-After headers
- Graceful fallbacks
- User notification

## Monitoring and Analytics

### 1. 📊 Usage Tracking

```javascript
{
  "monitoring": {
    "rateLimits": {
      "track": [
        "requests_per_second",
        "limit_exceeded_count",
        "usage_percentage"
      ],
      "alerts": {
        "threshold": 0.8,
        "notification": "email"
      }
    }
  }
}
```

### 2. 📈 Analytics Dashboard

```
Navigation: Dashboard → Rate Limits
```
- Real-time usage graphs
- Limit breach alerts
- Usage patterns
- Client statistics

## Troubleshooting

### Common Issues

1. **Unexpected Limiting**
   - Verify limit configuration
   - Check client identification
   - Review rate calculations
   - Monitor system time

2. **Performance Impact**
   - Optimize storage method
   - Use efficient algorithms
   - Configure appropriate windows
   - Monitor system resources

## Next Steps

- Explore [Response Caching](caching.md)
- Learn about [Monitoring](monitoring.md)
- Review [Best Practices](../guides/best-practices.md)

---

<div align="center">

**[← Monitoring](monitoring.md)** | **[Response Caching →](caching.md)**

</div>