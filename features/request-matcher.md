# Request Matcher

<div align="center">

# 🎯 Request Matcher
### Precise API Response Control Through Advanced Request Matching

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/request-matcher)
[![Use Case](https://img.shields.io/badge/Use%20Case-Routing-blue?style=for-the-badge)](https://docs.mockgee.com/features/request-matcher)

</div>

## Overview

The Request Matcher is a powerful feature that allows you to configure how Mockgee responds to different API requests. Match requests based on path parameters, query strings, headers, and payload content to return specific responses.

## Matching Capabilities

### 🛣️ Path Parameters
Match dynamic segments in URL paths:

```javascript
// Configuration
{
  "path": "/api/users/{userId}/profile",
  "pathParams": {
    "userId": "12345"
  },
  "response": {
    "name": "John Doe",
    "email": "john@example.com"
  }
}

// Matches
GET /api/users/12345/profile
```

### 🔍 Query String Matching

#### Static Query Matching
```javascript
// Configuration
{
  "path": "/api/products",
  "queryParams": {
    "category": "electronics",
    "sort": "price"
  }
}

// Matches
GET /api/products?category=electronics&sort=price
```

#### Dynamic Query Matching
```javascript
// Configuration
{
  "path": "/api/users",
  "queryParams": "*"
}

// Matches any query parameters
GET /api/users?any=parameter&will=match
```

### 📋 Header Matching

```javascript
// Configuration
{
  "headers": {
    "Authorization": "Bearer *",
    "Content-Type": "application/json",
    "x-api-version": "1.0"
  }
}

// Matches
Headers:
Authorization: Bearer xyz123
Content-Type: application/json
x-api-version: 1.0
```

### 📦 Payload Matching

#### Full Payload Match
```javascript
// Configuration
{
  "method": "POST",
  "payload": {
    "type": "premium",
    "quantity": 5,
    "options": {
      "color": "blue"
    }
  }
}

// Must match exactly
POST /api/orders
{
  "type": "premium",
  "quantity": 5,
  "options": {
    "color": "blue"
  }
}
```

#### Specific Field Match
```javascript
// Configuration
{
  "matchFields": ["id", "type"],
  "payload": {
    "id": "12345",
    "type": "standard"
  }
}

// Matches (other fields ignored)
{
  "id": "12345",
  "type": "standard",
  "anyOtherField": "ignored"
}
```

#### Field Ignoring
```javascript
// Configuration
{
  "ignoreFields": ["timestamp", "requestId"],
  "payload": {
    "action": "process",
    "data": "important"
  }
}

// Matches (specified fields ignored)
{
  "action": "process",
  "data": "important",
  "timestamp": "any-value",
  "requestId": "any-value"
}
```

## Advanced Features

### 1. Combined Matching
```javascript
{
  "path": "/api/orders/{orderId}",
  "pathParams": {
    "orderId": "ORD-*"
  },
  "headers": {
    "Authorization": "Bearer *"
  },
  "queryParams": {
    "include": "details"
  }
}
```

### 2. Regular Expressions
```javascript
{
  "path": "/api/products/{productId}",
  "pathParams": {
    "productId": "^PRD-\\d{6}$"
  }
}
```

### 3. Nested Object Matching
```javascript
{
  "payload": {
    "user": {
      "profile": {
        "type": "premium"
      }
    }
  }
}
```

## Best Practices

### 1. Matcher Organization
- Order matchers from most specific to least specific
- Group related matchers together
- Use clear naming conventions

### 2. Path Parameters
- Use descriptive parameter names
- Consider using regex for complex patterns
- Provide fallback matches

### 3. Query Parameters
- Handle optional parameters appropriately
- Consider parameter order variations
- Use wildcards judiciously

### 4. Headers
- Case-sensitive matching
- Handle optional headers
- Consider common variations

### 5. Payload
- Match only necessary fields
- Handle nested objects carefully
- Consider data type variations

## Troubleshooting

### Common Issues

1. **Match Not Working**
   - Verify exact path structure
   - Check case sensitivity
   - Validate regex patterns

2. **Multiple Matches**
   - Review matcher order
   - Check specificity levels
   - Verify matching rules

## Examples

### Authentication Flow
```javascript
{
  "path": "/api/auth",
  "method": "POST",
  "headers": {
    "Content-Type": "application/json"
  },
  "payload": {
    "username": "*",
    "password": "*"
  },
  "responses": [
    {
      "match": {
        "payload": {
          "username": "valid_user",
          "password": "correct_pass"
        }
      },
      "response": {
        "status": 200,
        "body": {
          "token": "$$.uuid"
        }
      }
    }
  ]
}
```

### Complex Product Search
```javascript
{
  "path": "/api/products/search",
  "method": "GET",
  "queryParams": {
    "category": "*",
    "minPrice": "^\\d+(\\.\\d{1,2})?$",
    "maxPrice": "^\\d+(\\.\\d{1,2})?$",
    "sort": "^(price|rating)_(asc|desc)$"
  }
}
```

## Next Steps

- Explore [Dynamic Mock](dynamic-mock.md) for response generation
- Learn about [Fake Data](fake-data.md) for realistic responses
- Check [Best Practices](../guides/best-practices.md) for more tips

---

<div align="center">

**[← Dynamic Mock](dynamic-mock.md)** | **[Fake Data →](fake-data.md)**

</div>