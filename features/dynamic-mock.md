# Dynamic Mock

<div align="center">

# 🎭 Dynamic Mock
### Create Realistic and Dynamic API Responses

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/dynamic-mock)
[![Use Case](https://img.shields.io/badge/Use%20Case-Testing-blue?style=for-the-badge)](https://docs.mockgee.com/features/dynamic-mock)

</div>

## Overview

Dynamic Mocking in Mockgee allows you to create flexible, realistic API responses that can adapt based on request parameters. Instead of static responses, you can simulate real-world API behavior with dynamic data and conditional responses.

## Key Features

### 🔄 Multiple Response Configurations
- Configure different responses for the same endpoint
- Runtime response selection based on request criteria
- Support for complex matching patterns

### 🎯 Request-Based Response Selection
- Match based on headers, query parameters, or body content
- Support for path parameters and dynamic routing
- Conditional response selection

### 🧪 Test Scenario Support
- Simulate error cases and edge conditions
- Generate realistic test data
- Create comprehensive test suites

## Implementation Guide

### Basic Dynamic Mock

```javascript
// Configure endpoint: GET /api/user/{userId}
{
  "endpoint": "/api/user/{userId}",
  "method": "GET",
  "responses": [
    {
      "matcher": {
        "userId": "123"
      },
      "response": {
        "status": 200,
        "body": {
          "id": "123",
          "name": "John Doe",
          "type": "premium"
        }
      }
    },
    {
      "matcher": {
        "userId": "456"
      },
      "response": {
        "status": 200,
        "body": {
          "id": "456",
          "name": "Jane Smith",
          "type": "basic"
        }
      }
    }
  ]
}
```

### Advanced Scenarios

#### Error Simulation
```javascript
{
  "endpoint": "/api/orders",
  "method": "POST",
  "responses": [
    {
      "matcher": {
        "headers": {
          "Authorization": "Bearer invalid"
        }
      },
      "response": {
        "status": 401,
        "body": {
          "error": "Invalid authentication token",
          "code": "AUTH_001"
        }
      }
    },
    {
      "matcher": {
        "body": {
          "amount": ">1000"
        }
      },
      "response": {
        "status": 400,
        "body": {
          "error": "Amount exceeds maximum limit",
          "code": "VAL_002"
        }
      }
    }
  ]
}
```

#### Dynamic Data Generation
```javascript
{
  "endpoint": "/api/transactions",
  "method": "GET",
  "response": {
    "status": 200,
    "body": {
      "transactionId": "$$.uuid",
      "timestamp": "$$.timestamp",
      "amount": "$$.float(4,2)",
      "status": "$$.enum(pending,completed,failed)",
      "reference": "$$.int(8)"
    }
  }
}
```

## Best Practices

### 1. Response Organization
- Group related responses together
- Use meaningful names for response configurations
- Document the purpose of each response variation

### 2. Request Matching
- Start with specific matchers before generic ones
- Use appropriate matching criteria (headers, query params, body)
- Include default responses for unmatched requests

### 3. Error Handling
- Include common error scenarios
- Use appropriate HTTP status codes
- Provide meaningful error messages

## Common Use Cases

### 1. User Authentication Flow
```javascript
// POST /api/login
{
  "responses": [
    {
      "matcher": {
        "body": {
          "username": "valid_user",
          "password": "correct_pass"
        }
      },
      "response": {
        "status": 200,
        "body": {
          "token": "$$.uuid",
          "expiresIn": 3600
        }
      }
    },
    {
      "matcher": {
        "body": {
          "username": "*",
          "password": "*"
        }
      },
      "response": {
        "status": 401,
        "body": {
          "error": "Invalid credentials"
        }
      }
    }
  ]
}
```

### 2. Conditional Business Logic
```javascript
// GET /api/pricing
{
  "responses": [
    {
      "matcher": {
        "query": {
          "region": "US",
          "tier": "premium"
        }
      },
      "response": {
        "price": 99.99,
        "currency": "USD"
      }
    },
    {
      "matcher": {
        "query": {
          "region": "EU",
          "tier": "premium"
        }
      },
      "response": {
        "price": 89.99,
        "currency": "EUR"
      }
    }
  ]
}
```

## Troubleshooting

### Common Issues

1. **Response Not Matching**
   - Verify matcher configuration
   - Check request format matches exactly
   - Confirm header case sensitivity

2. **Dynamic Data Issues**
   - Validate dynamic data syntax
   - Check supported data types
   - Verify format specifications

## Next Steps

- Explore [Request Matcher](request-matcher.md) for advanced matching
- Learn about [Fake Data](fake-data.md) generation
- Check [Best Practices](../guides/best-practices.md) for more tips

---

<div align="center">

**[← Back to Features](../features/README.md)** | **[Request Matcher →](request-matcher.md)**

</div>