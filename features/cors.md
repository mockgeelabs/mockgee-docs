# CORS Support

<div align="center">

# 🌐 CORS Support
### Seamless Cross-Origin Resource Sharing

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/cors)
[![Use Case](https://img.shields.io/badge/Use%20Case-Web_Integration-blue?style=for-the-badge)](https://docs.mockgee.com/features/cors)

</div>

## Overview

Mockgee provides built-in Cross-Origin Resource Sharing (CORS) support, enabling seamless integration with web applications running on different domains. Configure CORS settings easily to test your frontend applications against mock APIs.

## Quick Setup

### Basic CORS Configuration
```javascript
{
    "cors": {
        "enabled": true,
        "allowedOrigins": ["*"],
        "allowedMethods": ["GET", "POST", "PUT", "DELETE"],
        "allowedHeaders": ["Content-Type", "Authorization"],
        "exposedHeaders": ["X-Custom-Header"],
        "maxAge": 3600,
        "allowCredentials": true
    }
}
```

## Configuration Options

### 🎯 Allowed Origins
Control which domains can access your mock API:

```javascript
// Allow specific domains
{
    "allowedOrigins": [
        "https://app.example.com",
        "https://dev.example.com"
    ]
}

// Allow all origins
{
    "allowedOrigins": ["*"]
}

// Allow with wildcards
{
    "allowedOrigins": [
        "https://*.example.com",
        "http://localhost:*"
    ]
}
```

### 🛠️ HTTP Methods
Specify allowed HTTP methods:

```javascript
{
    "allowedMethods": [
        "GET",
        "POST",
        "PUT",
        "DELETE",
        "PATCH",
        "OPTIONS"
    ]
}
```

### 📋 Headers Configuration
Control header access:

```javascript
{
    // Headers that can be used in requests
    "allowedHeaders": [
        "Content-Type",
        "Authorization",
        "X-Requested-With",
        "Accept"
    ],
    
    // Headers exposed to client
    "exposedHeaders": [
        "X-Custom-Header",
        "X-Rate-Limit"
    ]
}
```

### ⚙️ Advanced Options

```javascript
{
    // Preflight cache duration (in seconds)
    "maxAge": 3600,
    
    // Allow credentials (cookies, authorization headers)
    "allowCredentials": true,
    
    // Enable automatic OPTIONS handling
    "handlePreflight": true
}
```

## Implementation Examples

### 1. Development Environment
```javascript
{
    "cors": {
        "enabled": true,
        "allowedOrigins": [
            "http://localhost:3000",
            "http://localhost:8000"
        ],
        "allowedMethods": ["*"],
        "allowedHeaders": ["*"],
        "maxAge": 86400
    }
}
```

### 2. Production Configuration
```javascript
{
    "cors": {
        "enabled": true,
        "allowedOrigins": [
            "https://app.production.com",
            "https://*.trusted-domain.com"
        ],
        "allowedMethods": [
            "GET",
            "POST",
            "PUT",
            "DELETE"
        ],
        "allowedHeaders": [
            "Content-Type",
            "Authorization"
        ],
        "maxAge": 3600,
        "allowCredentials": true
    }
}
```

### 3. Testing Configuration
```javascript
{
    "cors": {
        "enabled": true,
        "allowedOrigins": ["*"],
        "allowedMethods": ["*"],
        "allowedHeaders": ["*"],
        "exposedHeaders": ["*"],
        "maxAge": 0,
        "allowCredentials": false
    }
}
```

## Best Practices

### 1. Security
- Avoid using `"*"` in production
- Limit exposed headers
- Configure appropriate maxAge
- Use HTTPS in production

### 2. Performance
- Set appropriate cache duration
- Enable preflight caching
- Optimize allowed methods

### 3. Development
- Use specific origins
- Enable detailed logging
- Test all CORS scenarios

## Common Scenarios

### 1. Frontend Development
```javascript
{
    "cors": {
        "enabled": true,
        "allowedOrigins": [
            "http://localhost:3000",
            "http://127.0.0.1:3000"
        ],
        "allowedMethods": ["*"],
        "allowCredentials": true
    }
}
```

### 2. Microservices Testing
```javascript
{
    "cors": {
        "enabled": true,
        "allowedOrigins": [
            "https://service1.local",
            "https://service2.local"
        ],
        "allowedHeaders": [
            "Content-Type",
            "X-Service-ID"
        ]
    }
}
```

## Troubleshooting

### Common Issues

1. **Preflight Failures**
   - Verify OPTIONS handling
   - Check allowed methods
   - Confirm header configurations

2. **Authentication Issues**
   - Check allowCredentials setting
   - Verify Authorization header
   - Confirm origin configuration

3. **Browser Errors**
   - Review console messages
   - Check origin matching
   - Verify header configurations

## Next Steps

- Explore [Proxy Mode](proxy.md) for advanced routing
- Learn about [Request Matcher](request-matcher.md)
- Check [Best Practices](../guides/best-practices.md)

---

<div align="center">

**[← Importers](importers.md)** | **[Proxy Mode →](proxy.md)**

</div>