# Proxy Mode

<div align="center">

# 🔄 Proxy Mode
### Seamless Request Forwarding and Real API Integration

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/proxy)
[![Use Case](https://img.shields.io/badge/Use%20Case-Hybrid_Testing-blue?style=for-the-badge)](https://docs.mockgee.com/features/proxy)

</div>

## Overview

Proxy Mode enables Mockgee to forward requests to real APIs when no matching mock is found. This creates a hybrid testing environment where you can selectively mock certain endpoints while allowing others to pass through to actual services.

## Key Features

### 🎯 Smart Request Routing
- Automatic fallback to real APIs
- Selective endpoint proxying
- Request transformation support

### 🔄 Response Handling
- Response caching
- Error handling
- Headers preservation

### 🛠️ Configuration Options
- Target URL mapping
- Authentication forwarding
- Request modification

## Configuration Guide

### Basic Proxy Setup

```javascript
{
    "proxy": {
        "enabled": true,
        "target": "https://api.example.com",
        "preserveHostHeader": true,
        "timeout": 5000
    }
}
```

### Advanced Configuration

```javascript
{
    "proxy": {
        "enabled": true,
        "target": "https://api.example.com",
        "paths": {
            "/users/*": "https://users.example.com",
            "/orders/*": "https://orders.example.com"
        },
        "headers": {
            "forward": ["Authorization", "User-Agent"],
            "add": {
                "X-Proxy-By": "Mockgee"
            }
        },
        "options": {
            "timeout": 5000,
            "followRedirects": true,
            "preserveHostHeader": true
        }
    }
}
```

## Implementation Examples

### 1. Basic API Proxy
```javascript
{
    "endpoint": "/api/users",
    "proxy": {
        "target": "https://api.example.com",
        "enabled": true
    }
}
```

### 2. Multiple Service Routing
```javascript
{
    "proxy": {
        "enabled": true,
        "routes": [
            {
                "path": "/api/users/*",
                "target": "https://users-service.example.com"
            },
            {
                "path": "/api/orders/*",
                "target": "https://orders-service.example.com"
            }
        ]
    }
}
```

### 3. Authentication Handling
```javascript
{
    "proxy": {
        "target": "https://api.secure.com",
        "auth": {
            "type": "bearer",
            "token": "API_TOKEN",
            "forward": true
        },
        "headers": {
            "forward": ["Authorization"],
            "add": {
                "X-API-Key": "proxy-key"
            }
        }
    }
}
```

## Advanced Features

### 🔄 Request Transformation
Transform requests before forwarding:

```javascript
{
    "proxy": {
        "target": "https://api.example.com",
        "transform": {
            "request": {
                "headers": {
                    "remove": ["X-Original-Header"],
                    "add": {
                        "X-Proxy-Version": "1.0"
                    }
                },
                "params": {
                    "add": {
                        "version": "v2"
                    }
                }
            }
        }
    }
}
```

### 📝 Response Modification
Modify responses before returning:

```javascript
{
    "proxy": {
        "transform": {
            "response": {
                "headers": {
                    "remove": ["X-Internal-Header"],
                    "add": {
                        "X-Modified-By": "Mockgee"
                    }
                },
                "body": {
                    "wrap": {
                        "success": true,
                        "data": "$response"
                    }
                }
            }
        }
    }
}
```

### 🎯 Conditional Proxying
Route based on conditions:

```javascript
{
    "proxy": {
        "conditions": [
            {
                "if": {
                    "headers": {
                        "X-Environment": "prod"
                    }
                },
                "then": {
                    "target": "https://prod-api.example.com"
                }
            },
            {
                "if": {
                    "headers": {
                        "X-Environment": "dev"
                    }
                },
                "then": {
                    "target": "https://dev-api.example.com"
                }
            }
        ]
    }
}
```

## Best Practices

### 1. Security
- Use HTTPS for target URLs
- Configure appropriate timeouts
- Implement rate limiting
- Handle sensitive headers

### 2. Performance
- Enable response caching
- Set reasonable timeouts
- Monitor proxy status

### 3. Reliability
- Implement fallback options
- Handle connection errors
- Log proxy activities

## Common Use Cases

### 1. Development Environment
```javascript
{
    "proxy": {
        "enabled": true,
        "target": "https://dev-api.example.com",
        "options": {
            "timeout": 10000,
            "logging": true,
            "caching": {
                "enabled": true,
                "duration": 300
            }
        }
    }
}
```

### 2. Testing Environment
```javascript
{
    "proxy": {
        "enabled": true,
        "target": "https://test-api.example.com",
        "options": {
            "recordMode": true,
            "generateMocks": true,
            "fallbackToMock": true
        }
    }
}
```

## Troubleshooting

### Common Issues

1. **Connection Failures**
   - Verify target URL
   - Check network connectivity
   - Review SSL certificates

2. **Authentication Issues**
   - Verify token forwarding
   - Check header preservation
   - Confirm credentials

3. **Timeout Problems**
   - Adjust timeout settings
   - Monitor response times
   - Implement retry logic

## Next Steps

- Explore [CORS Support](cors.md) for web integration
- Learn about [Request Matcher](request-matcher.md)
- Check [Best Practices](../guides/best-practices.md)

---

<div align="center">

**[← CORS Support](cors.md)** | **[Dynamic Mock →](dynamic-mock.md)**

</div>