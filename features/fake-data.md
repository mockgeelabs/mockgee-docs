# Fake Data

<div align="center">

# 🎲 Fake Data Generator
### Generate Dynamic, Realistic Test Data on the Fly

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/faker)
[![Use Case](https://img.shields.io/badge/Use%20Case-Testing-blue?style=for-the-badge)](https://docs.mockgee.com/features/faker)

</div>

## Overview

The Fake Data Generator in Mockgee allows you to create dynamic, realistic test data for your API mocks. Using simple syntax with the `$$.` prefix, you can generate various types of data that changes with each API call.

## Data Types at a Glance

| Type | Description | Example Usage | Sample Output |
|------|-------------|---------------|---------------|
| uuid | Unique identifier | `$$.uuid` | "123e4567-e89b-12d3-a456-426614174000" |
| ip | IP address | `$$.ip` | "192.168.1.1" |
| name | Random name | `$$.name` | "John Smith" |
| int | Integer number | `$$.int(6)` | 123456 |
| float | Decimal number | `$$.float(4,2)` | 12.34 |
| timestamp | Current time | `$$.timestamp` | "2024-02-28T12:25:41.994Z" |
| boolean | True/false value | `$$.boolean` | true |
| enum | Custom values | `$$.enum(red,green,blue)` | "green" |

## Implementation Guide

### Basic Usage

```json
{
    "userId": "$$.uuid",
    "createdAt": "$$.timestamp",
    "profile": {
        "name": "$$.name",
        "isActive": "$$.boolean",
        "loginCount": "$$.int(3)"
    }
}
```

### JSON Response Example

```json
{
    "order": {
        "id": "$$.uuid",
        "customer": {
            "id": "$$.int(6)",
            "name": "$$.name",
            "email": "customer@example.com"
        },
        "amount": "$$.float(4,2)",
        "status": "$$.enum(pending,processing,completed)",
        "ipAddress": "$$.ip",
        "timestamp": "$$.timestamp"
    }
}
```

### XML Response Example

```xml
<?xml version="1.0"?>
<order>
    <id>$$.uuid</id>
    <customerInfo>
        <name>$$.name</name>
        <status>$$.enum(active,inactive)</status>
    </customerInfo>
    <amount>$$.float(5,2)</amount>
    <isUrgent>$$.boolean</isUrgent>
</order>
```

## Detailed Data Types

### 📑 UUID Generator
Generate universally unique identifiers.
```javascript
{
    "transactionId": "$$.uuid"  // "550e8400-e29b-41d4-a716-446655440000"
}
```

### 🌐 IP Address
Generate valid IP addresses.
```javascript
{
    "sourceIp": "$$.ip"  // "192.168.1.1"
}
```

### 👤 Name Generator
Generate random names.
```javascript
{
    "firstName": "$$.name",  // "John"
    "lastName": "$$.name"    // "Smith"
}
```

### 🔢 Number Generators

#### Integer (int)
Generate whole numbers with specific length.
```javascript
{
    "shortCode": "$$.int(3)",     // 123
    "accountNumber": "$$.int(8)"  // 12345678
}
```

#### Integer String (ints)
Generate numbers in string format.
```javascript
{
    "zipCode": "$$.ints(5)",      // "12345"
    "phoneNumber": "$$.ints(10)"  // "1234567890"
}
```

#### Float
Generate decimal numbers with specified precision.
```javascript
{
    "price": "$$.float(4,2)",    // 12.34
    "quantity": "$$.float(3,1)"  // 1.5
}
```

### ⏰ Timestamp
Generate current timestamp in ISO format.
```javascript
{
    "createdAt": "$$.timestamp",  // "2024-02-28T12:25:41.994Z"
    "updatedAt": "$$.timestamp"   // "2024-02-28T12:25:41.994Z"
}
```

### ✅ Boolean
Generate random true/false values.
```javascript
{
    "isActive": "$$.boolean",    // true
    "isEnabled": "$$.boolean"    // false
}
```

### 📝 Enum
Generate values from a predefined set.
```javascript
{
    "status": "$$.enum(active,pending,inactive)",
    "priority": "$$.enum(high,medium,low)",
    "category": "$$.enum(electronics,books,clothing)"
}
```

## Advanced Usage

### Combining Multiple Types
```json
{
    "transaction": {
        "id": "$$.uuid",
        "amount": "$$.float(6,2)",
        "status": "$$.enum(pending,completed,failed)",
        "timestamp": "$$.timestamp",
        "customer": {
            "id": "$$.int(6)",
            "ipAddress": "$$.ip",
            "isVerified": "$$.boolean"
        }
    }
}
```

### Complex Data Structures
```json
{
    "orders": [
        {
            "orderId": "$$.uuid",
            "items": [
                {
                    "productId": "$$.int(5)",
                    "quantity": "$$.int(2)",
                    "price": "$$.float(4,2)"
                },
                {
                    "productId": "$$.int(5)",
                    "quantity": "$$.int(2)",
                    "price": "$$.float(4,2)"
                }
            ],
            "status": "$$.enum(new,processing,shipped)",
            "isExpedited": "$$.boolean"
        }
    ]
}
```

## Best Practices

### 1. Data Consistency
- Use consistent data types across related fields
- Maintain realistic value ranges
- Consider data relationships

### 2. Performance
- Use appropriate field lengths
- Balance complexity with response time
- Consider payload size

### 3. Realism
- Use appropriate data types for fields
- Maintain logical relationships
- Consider business rules

## Troubleshooting

### Common Issues

1. **Invalid Data Generation**
   - Verify syntax format
   - Check supported data types
   - Validate parameter ranges

2. **Inconsistent Data**
   - Review data type specifications
   - Check format parameters
   - Verify enum values

## Next Steps

- Learn about [Dynamic Mock](dynamic-mock.md) for complex scenarios
- Explore [Request Matcher](request-matcher.md) for request handling
- Check [Best Practices](../guides/best-practices.md) for more tips

---

<div align="center">

**[← Request Matcher](request-matcher.md)** | **[Importers →](importers.md)**

</div>