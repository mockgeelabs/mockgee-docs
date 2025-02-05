# Response Caching

<div align="center">

# 🚀 Response Caching
### Optimize Performance with Smart Caching

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/caching)
[![Use Case](https://img.shields.io/badge/Use%20Case-Performance-blue?style=for-the-badge)](https://docs.mockgee.com/features/caching)

</div>

## Overview

Mockgee's Response Caching feature optimizes performance by storing and serving frequently requested responses. Configure caching strategies to reduce response time and server load.

## Key Features

### 🎯 Caching Strategies
- Time-based caching
- Request-based caching
- Conditional caching
- Cache invalidation

### 🔄 Cache Types
- In-memory cache
- Distributed cache
- Custom storage
- Hybrid caching

## Implementation Guide

### 1. Basic Caching

```javascript
{
  "caching": {
    "enabled": true,
    "ttl": "1h",
    "storage": "memory"
  }
}
```

### 2. Per-Endpoint Configuration

```javascript
{
  "endpoint": "/api/products",
  "caching": {
    "enabled": true,
    "strategy": {
      "type": "time",
      "duration": "15m",
      "vary": ["Accept", "Accept-Language"]
    }
  }
}
```

### 3. Advanced Cache Rules

```javascript
{
  "caching": {
    "rules": [
      {
        "matcher": {
          "path": "/api/static/*",
          "method": "GET"
        },
        "config": {
          "ttl": "24h",
          "maxSize": "100MB"
        }
      },
      {
        "matcher": {
          "path": "/api/dynamic/*",
          "method": "GET"
        },
        "config": {
          "ttl": "5m",
          "staleWhileRevalidate": "1m"
        }
      }
    ]
  }
}
```

## Advanced Features

### 1. 🎯 Conditional Caching

```javascript
{
  "caching": {
    "conditional": {
      "rules": [
        {
          "if": "request.headers['user-type'] === 'premium'",
          "then": {
            "ttl": "1h",
            "private": true
          }
        },
        {
          "if": "response.headers['content-type'].includes('image')",
          "then": {
            "ttl": "7d",
            "public": true
          }
        }
      ]
    }
  }
}
```

### 2. 🔄 Cache Control

```javascript
{
  "caching": {
    "control": {
      "maxAge": 3600,
      "staleWhileRevalidate": 300,
      "staleIfError": 86400,
      "mustRevalidate": true,
      "proxyRevalidate": true
    }
  }
}
```

### 3. 📊 Cache Groups

```javascript
{
  "caching": {
    "groups": {
      "static": {
        "ttl": "7d",
        "paths": ["/images/*", "/assets/*"],
        "headers": {
          "Cache-Control": "public, max-age=604800"
        }
      },
      "dynamic": {
        "ttl": "5m",
        "paths": ["/api/data/*"],
        "vary": ["Authorization"]
      }
    }
  }
}
```

## Cache Management

### 1. Invalidation Strategies

```javascript
{
  "caching": {
    "invalidation": {
      "patterns": [
        {
          "trigger": "POST /api/products/*",
          "invalidate": [
            "GET /api/products",
            "GET /api/products/*"
          ]
        }
      ],
      "methods": {
        "manual": true,
        "automatic": true,
        "scheduled": true
      }
    }
  }
}
```

### 2. Cache Warmup

```javascript
{
  "caching": {
    "warmup": {
      "enabled": true,
      "strategies": [
        {
          "path": "/api/popular/*",
          "frequency": "1h",
          "priority": "high"
        }
      ]
    }
  }
}
```

### 3. Storage Configuration

```javascript
{
  "caching": {
    "storage": {
      "type": "hybrid",
      "layers": [
        {
          "type": "memory",
          "maxSize": "1GB",
          "priority": 1
        },
        {
          "type": "redis",
          "connection": "redis://localhost:6379",
          "priority": 2
        }
      ]
    }
  }
}
```

## Headers and Responses

### Cache Headers

```http
Cache-Control: public, max-age=3600
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"
Last-Modified: Wed, 05 Feb 2024 12:00:00 GMT
```

### Cached Response

```javascript
{
  "data": {
    // Response data
  },
  "cache": {
    "hit": true,
    "age": 120,
    "ttl": 3600,
    "key": "cache-key-123"
  }
}
```

## Best Practices

### 1. Configuration Strategy
- Cache appropriate content
- Set proper TTL values
- Use appropriate storage
- Implement validation

### 2. Performance Tips
- Use layered caching
- Implement cache warming
- Monitor hit rates
- Regular maintenance

### 3. Security Considerations
- Cache safe data only
- Implement access control
- Secure cache storage
- Regular security audits

## Monitoring and Analytics

### 1. Cache Metrics

```javascript
{
  "monitoring": {
    "cache": {
      "metrics": [
        "hit_rate",
        "miss_rate",
        "eviction_rate",
        "memory_usage"
      ],
      "alerts": {
        "lowHitRate": 0.5,
        "highMemoryUsage": 0.8
      }
    }
  }
}
```

### 2. Analytics Dashboard

```
Navigation: Dashboard → Cache Analytics
```
- Hit/Miss ratios
- Cache size
- Popular entries
- Performance impact

## Troubleshooting

### Common Issues

1. **Cache Misses**
   - Verify cache configuration
   - Check TTL settings
   - Review invalidation rules
   - Monitor storage capacity

2. **Performance Issues**
   - Optimize cache size
   - Review storage type
   - Check network latency
   - Monitor memory usage

## Next Steps

- Learn about [Rate Limiting](rate-limiting.md)
- Explore [Monitoring](monitoring.md)
- Review [Best Practices](../guides/best-practices.md)

---

<div align="center">

**[← Rate Limiting](rate-limiting.md)** | **[Monitoring →](monitoring.md)**

</div>