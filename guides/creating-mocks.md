# Creating Mocks

<div align="center">

# 🎯 Creating Mock APIs
### A Complete Guide to Creating and Managing Mocks in Mockgee

[![Guide Type](https://img.shields.io/badge/Guide-Getting_Started-success?style=for-the-badge)](https://docs.mockgee.com/guides/creating-mocks)
[![Level](https://img.shields.io/badge/Level-Beginner-blue?style=for-the-badge)](https://docs.mockgee.com/guides/creating-mocks)

</div>

## Overview

This guide walks you through the process of creating mock APIs in Mockgee, from basic endpoints to complex scenarios with dynamic responses and request matching.

## Quick Start

### Creating Your First Mock

1. **Access Mock Creation**
   ```
   Navigation: Mock → Add New Mock
   ```

2. **Basic Configuration**
   ```javascript
   {
     "endpoint": "/api/hello",
     "method": "GET",
     "response": {
       "status": 200,
       "body": {
         "message": "Hello, World!"
       }
     }
   }
   ```

## Methods of Creation

### 1. 📝 Manual Creation

#### Step-by-Step Process

1. **Define Endpoint Details**
   ```javascript
   {
     "name": "User Profile API",
     "endpoint": "/api/users/{userId}",
     "method": "GET"
   }
   ```

2. **Configure Response**
   ```javascript
   {
     "response": {
       "status": 200,
       "headers": {
         "Content-Type": "application/json"
       },
       "body": {
         "id": "$$.uuid",
         "name": "$$.name",
         "email": "user@example.com"
       }
     }
   }
   ```

3. **Add Request Matchers**
   ```javascript
   {
     "matchers": {
       "params": {
         "userId": "12345"
       },
       "headers": {
         "Authorization": "Bearer *"
       }
     }
   }
   ```

### 2. 📥 Import from Specification

#### Using OpenAPI/Swagger
```javascript
// 1. Navigate to Importer
Mock → Importer → OpenAPI

// 2. Upload or paste specification
{
  "openapi": "3.0.0",
  "info": {
    "title": "Sample API",
    "version": "1.0.0"
  },
  "paths": {
    "/users": {
      "get": {
        "responses": {
          "200": {
            "description": "Success"
          }
        }
      }
    }
  }
}
```

#### Using Postman Collection
```javascript
// 1. Export collection from Postman
// 2. Import in Mockgee
Mock → Importer → Postman Collection
```

### 3. 🔄 API Recording

1. **Configure Proxy**
   ```javascript
   {
     "recording": {
       "target": "https://api.example.com",
       "enabled": true,
       "saveResponses": true
     }
   }
   ```

2. **Start Recording**
   ```
   Mock → Record → Start Recording
   ```

## Advanced Mock Creation

### 1. Dynamic Response Configuration

```javascript
{
  "endpoint": "/api/users",
  "method": "POST",
  "response": {
    "body": {
      "id": "$$.uuid",
      "createdAt": "$$.timestamp",
      "name": "$request.body.name",
      "type": "$$.enum(free,premium,enterprise)"
    }
  }
}
```

### 2. Multiple Response Scenarios

```javascript
{
  "endpoint": "/api/orders/{orderId}",
  "responses": [
    {
      "condition": {
        "params": {
          "orderId": "123"
        }
      },
      "response": {
        "status": 200,
        "body": {
          "id": "123",
          "status": "completed"
        }
      }
    },
    {
      "condition": {
        "params": {
          "orderId": "456"
        }
      },
      "response": {
        "status": 200,
        "body": {
          "id": "456",
          "status": "pending"
        }
      }
    }
  ]
}
```

### 3. Error Scenarios

```javascript
{
  "endpoint": "/api/secure/data",
  "responses": [
    {
      "condition": {
        "headers": {
          "Authorization": "Bearer valid-token"
        }
      },
      "response": {
        "status": 200,
        "body": {
          "data": "Secure content"
        }
      }
    },
    {
      "condition": {
        "headers": {
          "Authorization": "*"
        }
      },
      "response": {
        "status": 401,
        "body": {
          "error": "Invalid token"
        }
      }
    }
  ]
}
```

## Organization & Management

### 1. Project Structure
```
Mock Project
├── Authentication
│   ├── Login
│   ├── Logout
│   └── Reset Password
├── Users
│   ├── Get User
│   ├── Update User
│   └── Delete User
└── Orders
    ├── Create Order 
    └── Get Orders
```

### 2. Version Management
```javascript
{
  "endpoint": "/api/v1/users",
  "variants": [
    {
      "version": "v1",
      "response": {
        // Version 1 response
      }
    },
    {
      "version": "v2",
      "response": {
        // Version 2 response
      }
    }
  ]
}
```

## Testing Your Mocks

### 1. Using the Built-in Tester
```
Mock → Select Mock → Test
```

### 2. Using cURL
```bash
# Test GET endpoint
curl http://localhost:8085/api/hello

# Test POST endpoint
curl -X POST http://localhost:8085/api/users \
  -H "Content-Type: application/json" \
  -d '{"name": "John Doe"}'
```

### 3. Using Postman
1. Set URL to `http://localhost:8085/your-endpoint`
2. Configure method and headers
3. Send request

## Common Patterns

### 1. Authentication Flow
```javascript
{
  "endpoint": "/api/auth/login",
  "method": "POST",
  "response": {
    "body": {
      "token": "$$.uuid",
      "expiresIn": 3600,
      "user": {
        "id": "$request.body.username",
        "role": "$$.enum(user,admin)"
      }
    }
  }
}
```

### 2. CRUD Operations
```javascript
{
  "endpoint": "/api/resources",
  "methods": {
    "GET": {
      "response": {/* List response */}
    },
    "POST": {
      "response": {/* Create response */}
    },
    "PUT": {
      "response": {/* Update response */}
    },
    "DELETE": {
      "response": {/* Delete response */}
    }
  }
}
```

## Troubleshooting

### Common Issues

1. **Mock Not Matching**
   - Verify endpoint path
   - Check HTTP method
   - Validate request matchers

2. **Invalid Response**
   - Review response format
   - Check dynamic data syntax
   - Verify JSON structure

## Next Steps

- Explore [Dynamic Mock](../features/dynamic-mock.md)
- Learn about [Request Matcher](../features/request-matcher.md)
- Review [Best Practices](best-practices.md)

---

<div align="center">

**[← Setup Guide](../getting-started/setup.md)** | **[Best Practices →](best-practices.md)**

</div>