# Response Delay

<div align="center">

# ⏱️ Response Delay
### Simulate Network Conditions and API Response Times

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/delay)
[![Use Case](https://img.shields.io/badge/Use%20Case-Testing-blue?style=for-the-badge)](https://docs.mockgee.com/features/delay)

</div>

## Overview

The Response Delay feature allows you to simulate various network conditions and API response times. Test how your application handles slow responses, timeouts, and unreachable services.

## Key Features

### ⏱️ Delay Types
- Fixed delay duration
- Random delay ranges
- Conditional delays
- Global delay settings

### 🎯 Use Cases
- Timeout testing
- Loading state verification
- Error handling validation
- Network condition simulation

## Implementation Guide

### Basic Delay Configuration

```javascript
{
    "delay": {
        "enabled": true,
        "duration": 2000  // 2 seconds delay
    }
}
```

### Advanced Delay Scenarios

#### 1. Random Delay Range
```javascript
{
    "delay": {
        "enabled": true,
        "type": "random",
        "min": 1000,    // 1 second
        "max": 5000     // 5 seconds
    }
}
```

#### 2. Conditional Delay
```javascript
{
    "delay": {
        "conditions": [
            {
                "if": {
                    "headers": {
                        "X-Priority": "low"
                    }
                },
                "then": {
                    "duration": 5000  // 5 seconds delay
                }
            },
            {
                "if": {
                    "headers": {
                        "X-Priority": "high"
                    }
                },
                "then": {
                    "duration": 1000  // 1 second delay
                }
            }
        ]
    }
}
```

## Advanced Features

### 🔄 Dynamic Delay Patterns

#### Progressive Delay
Increase delay with each request:

```javascript
{
    "delay": {
        "type": "progressive",
        "start": 1000,
        "increment": 500,
        "max": 5000
    }
}
```

#### Pattern-Based Delay
Create specific delay patterns:

```javascript
{
    "delay": {
        "type": "pattern",
        "sequence": [1000, 2000, 5000, 0],
        "repeat": true
    }
}
```

### 🌐 Network Condition Simulation

```javascript
{
    "delay": {
        "networkCondition": {
            "type": "3g",  // Simulate 3G network
            "variance": 0.3 // 30% variance in delay
        }
    }
}
```

### ⚡ Load Testing Scenarios

```javascript
{
    "delay": {
        "loadPattern": {
            "type": "spike",
            "baseline": 1000,
            "peak": 5000,
            "duration": 60000  // 1 minute spike
        }
    }
}
```

## Best Practices

### 1. Testing Strategy
- Start with realistic delays
- Test various network conditions
- Include timeout scenarios
- Validate error handling

### 2. Implementation
- Use appropriate delay ranges
- Configure timeouts accordingly
- Handle all delay scenarios
- Log delay events

### 3. User Experience
- Show loading states
- Provide feedback
- Handle timeouts gracefully
- Implement retry logic

## Common Use Cases

### 1. Loading State Testing
```javascript
{
    "delay": {
        "enabled": true,
        "duration": 3000,  // 3 seconds
        "endpoints": [
            "/api/dashboard",
            "/api/reports"
        ]
    }
}
```

### 2. Timeout Testing
```javascript
{
    "delay": {
        "enabled": true,
        "duration": 30000,  // 30 seconds
        "conditions": {
            "probability": 0.1  // 10% chance of timeout
        }
    }
}
```

### 3. Network Simulation
```javascript
{
    "delay": {
        "networkProfiles": {
            "fast": {
                "latency": 50,
                "variance": 0.1
            },
            "slow": {
                "latency": 2000,
                "variance": 0.3
            },
            "unreliable": {
                "latency": 1000,
                "variance": 0.5,
                "errorRate": 0.1
            }
        }
    }
}
```

## Configuration Examples

### 1. Development Testing
```javascript
{
    "delay": {
        "enabled": true,
        "duration": 1000,
        "excludePaths": [
            "/api/health",
            "/api/metrics"
        ]
    }
}
```

### 2. Load Testing
```javascript
{
    "delay": {
        "enabled": true,
        "pattern": {
            "type": "gradual",
            "steps": [
                {"duration": 1000, "time": "0-10s"},
                {"duration": 2000, "time": "10-20s"},
                {"duration": 5000, "time": "20-30s"}
            ]
        }
    }
}
```

## Troubleshooting

### Common Issues

1. **Inconsistent Delays**
   - Check configuration
   - Verify network conditions
   - Monitor system resources

2. **Timeout Issues**
   - Review client timeouts
   - Check delay duration
   - Validate error handling

## Next Steps

- Explore [Dynamic Mock](dynamic-mock.md)
- Learn about [Request Matcher](request-matcher.md)
- Check [Response Mapping](mapping.md) feature

---

<div align="center">

**[← Response Mapping](mapping.md)** | **[Dynamic Mock →](dynamic-mock.md)**

</div>