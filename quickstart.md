# Quick Start

<div align="center">

# 🚀 Quick Start Guide
### Get Started with Mockgee in Minutes

[![Guide Type](https://img.shields.io/badge/Guide-Getting_Started-success?style=for-the-badge)](https://docs.mockgee.com/getting-started/quickstart)
[![Level](https://img.shields.io/badge/Level-Beginner-blue?style=for-the-badge)](https://docs.mockgee.com/getting-started/quickstart)

</div>

## Overview

Welcome to Mockgee! This guide will help you set up Mockgee and create your first mock API in minutes. Follow these simple steps to get started with API mocking.

## Installation Options

### 🐳 Using Docker (Recommended)

Get started instantly with our Docker image:

```bash
docker run -p 8080:8080 -p 8085:8085 mockgee/mockgee:latest
```

### 🐧 Ubuntu Installation

One-line installation for Ubuntu users:

```bash
curl -fsSL https://raw.githubusercontent.com/mockgeelabs/mockgee-install/main/mockgee.sh -o mockgee.sh && chmod +x mockgee.sh && ./mockgee.sh install
```

## Creating Your First Mock

### 1. 🖥️ Access the Dashboard
```
Open your browser → http://localhost:8080
```

### 2. 🆕 Create New Mock
```
Navigation: Mock → Add
```

### 3. ⚙️ Configure the Mock

```javascript
// Endpoint: GET /api/users/1
{
  "endpoint": "/api/users/1",
  "method": "GET",
  "response": {
    "status": 200,
    "body": {
      "id": 1,
      "name": "$$.name",
      "email": "user@example.com",
      "role": "$$.enum(admin,user,guest)"
    }
  }
}
```

### 4. ✅ Test Your Mock
```bash
# Your mock is available at:
curl http://localhost:8085/api/users/1
```

## Quick Examples

### 🎲 Dynamic Data Generation

```javascript
{
  "endpoint": "/api/orders",
  "method": "POST",
  "response": {
    "body": {
      "orderId": "$$.uuid",
      "amount": "$$.float(4,2)",
      "timestamp": "$$.timestamp",
      "status": "$$.enum(pending,processing,completed)"
    }
  }
}
```

### 🎯 Request Matching

```javascript
{
  "endpoint": "/api/orders",
  "method": "POST",
  "request": {
    "body": {
      "type": "premium",
      "quantity": 5
    }
  },
  "response": {
    "status": 200,
    "body": {
      "status": "success",
      "deliveryTime": "2 days"
    }
  }
}
```

## Advanced Features Preview

### 1. 🔄 Dynamic Response
```javascript
{
  "endpoint": "/api/profile",
  "method": "GET",
  "response": {
    "body": {
      "user": "$request.query.username",
      "lastLogin": "$$.timestamp",
      "status": "$$.enum(online,away,offline)"
    }
  }
}
```

### 2. 🎭 Multiple Scenarios
```javascript
{
  "endpoint": "/api/payment",
  "method": "POST",
  "scenarios": [
    {
      "name": "Success",
      "response": {
        "status": 200,
        "body": {
          "status": "approved"
        }
      }
    },
    {
      "name": "Failure",
      "response": {
        "status": 400,
        "body": {
          "error": "Insufficient funds"
        }
      }
    }
  ]
}
```

## Troubleshooting

### Common Issues

#### 1. 🔍 Port Conflicts
```bash
# Check if ports are in use
lsof -i :8080
lsof -i :8085

# Alternative ports
docker run -p 8081:8080 -p 8086:8085 mockgee/mockgee:latest
```

#### 2. 🐳 Docker Issues
```bash
# Check container status
docker ps -a | grep mockgee

# View logs
docker logs mockgee

# Restart container
docker restart mockgee
```

#### 3. 🔑 Permission Issues
```bash
# Fix permission issues
sudo chown -R $(whoami):$(whoami) ~/.mockgee
```

## Next Steps

- Dive into [Detailed Setup](setup.md)
- Explore [Dynamic Mocking](../features/dynamic-mock.md)
- Learn [Request Matching](../features/request-matcher.md)
- Review [Best Practices](../guides/best-practices.md)

## Quick Reference

### 🔧 Port Configuration
- UI Dashboard: 8080
- Mock API Endpoint: 8085

### 📁 Default Locations
- Configuration: ~/.mockgee/config
- Logs: ~/.mockgee/logs
- Data: ~/.mockgee/data

---

<div align="center">

**[← Introduction](../README.md)** | **[Setup Guide →](setup.md)**

</div>