# Response Mapping

<div align="center">

# 🔄 Response Mapping
### Inject Request Data into Mock Responses

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/mapping)
[![Use Case](https://img.shields.io/badge/Use%20Case-Dynamic_Response-blue?style=for-the-badge)](https://docs.mockgee.com/features/mapping)

</div>

## Overview

Response Mapping allows you to dynamically inject data from incoming requests into your mock responses. Use data from request payload, query parameters, or path parameters to create contextual responses.

## Key Features

### 🎯 Data Source Support
- Request body mapping
- Query parameter injection
- Path parameter usage
- Header value access

### 🔄 Mapping Syntax
Use `$request` to reference request data:
- `$request.body` - Access request payload
- `$request.query` - Access query parameters
- `$request.params` - Access path parameters
- `$request.headers` - Access request headers

## Implementation Guide

### Basic Mapping

```javascript
// Request
POST /api/users
{
    "name": "John Doe",
    "email": "john@example.com"
}

// Response Configuration
{
    "response": {
        "body": {
            "message": "Hello, $request.body.name!",
            "userEmail": "$request.body.email"
        }
    }
}

// Generated Response
{
    "message": "Hello, John Doe!",
    "userEmail": "john@example.com"
}
```

### Advanced Mapping Scenarios

#### 1. Nested Object Mapping
```javascript
// Request
POST /api/orders
{
    "order": {
        "items": [
            {
                "productId": "123",
                "quantity": 2
            }
        ],
        "shipping": {
            "address": "123 Main St"
        }
    }
}

// Response Configuration
{
    "response": {
        "body": {
            "confirmation": {
                "items": "$request.body.order.items",
                "shippingTo": "$request.body.order.shipping.address"
            }
        }
    }
}
```

#### 2. Query Parameter Mapping
```javascript
// Request
GET /api/search?category=books&sort=price

// Response Configuration
{
    "response": {
        "body": {
            "searchResults": [],
            "filters": {
                "appliedCategory": "$request.query.category",
                "sortOrder": "$request.query.sort"
            }
        }
    }
}
```

#### 3. Path Parameter Mapping
```javascript
// Request
GET /api/users/123/profile

// Response Configuration
{
    "response": {
        "body": {
            "userId": "$request.params.userId",
            "requestedAt": "$$.timestamp"
        }
    }
}
```

## Advanced Features

### 🔄 Conditional Mapping
Map different responses based on request data:

```javascript
{
    "response": {
        "body": {
            "status": {
                "if": "$request.body.type == 'premium'",
                "then": "Priority Processing",
                "else": "Standard Processing"
            },
            "estimatedTime": {
                "if": "$request.body.type == 'premium'",
                "then": "1-2 days",
                "else": "3-5 days"
            }
        }
    }
}
```

### 📝 Data Transformation
Transform request data before mapping:

```javascript
{
    "response": {
        "body": {
            "upperName": "$uppercase($request.body.name)",
            "formattedDate": "$formatDate($request.body.date, 'YYYY-MM-DD')",
            "totalPrice": "$multiply($request.body.quantity, $request.body.price)"
        }
    }
}
```

### 🔍 Complex Data Manipulation
Combine multiple request values:

```javascript
{
    "response": {
        "body": {
            "fullAddress": "$concat([
                $request.body.address.street,
                ', ',
                $request.body.address.city,
                ', ',
                $request.body.address.country
            ])"
        }
    }
}
```

## Best Practices

### 1. Data Validation
- Verify request data exists
- Provide default values
- Handle missing fields

### 2. Security
- Sanitize mapped data
- Validate data types
- Filter sensitive information

### 3. Performance
- Optimize mapping paths
- Use efficient transformations
- Cache when possible

## Common Use Cases

### 1. Form Submission Response
```javascript
// Request
POST /api/submit
{
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@example.com"
}

// Response Configuration
{
    "response": {
        "body": {
            "confirmation": {
                "message": "Thank you, $request.body.firstName $request.body.lastName!",
                "emailSentTo": "$request.body.email",
                "submittedAt": "$$.timestamp"
            }
        }
    }
}
```

### 2. Search API Response
```javascript
// Request
GET /api/search?term=example&page=1

// Response Configuration
{
    "response": {
        "body": {
            "searchTerm": "$request.query.term",
            "currentPage": "$request.query.page",
            "results": [],
            "metadata": {
                "query": "$request.query"
            }
        }
    }
}
```

## Troubleshooting

### Common Issues

1. **Missing Data**
   - Check request format
   - Verify mapping paths
   - Add default values

2. **Type Mismatches**
   - Validate data types
   - Use appropriate transformations
   - Check format consistency

## Next Steps

- Explore [Dynamic Mock](dynamic-mock.md)
- Learn about [Request Matcher](request-matcher.md)
- Check [Response Delay](delay.md) feature

---

<div align="center">

**[← Proxy Mode](proxy.md)** | **[Response Delay →](delay.md)**

</div>