# Welcome to Mockgee

<div align="center">

# 🚀 Mockgee
### The Leading API Mocking Solution for Modern Development

[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)](https://docs.mockgee.com/getting-started/setup#docker)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://docs.mockgee.com/getting-started/setup#ubuntu-os)

</div>

## Why Mockgee?

Mockgee is your comprehensive solution for API mocking needs, trusted by industry leaders. Whether you're developing new services, testing integrations, or maintaining existing APIs, Mockgee provides the tools you need for efficient development and testing.

### Key Benefits

- 🔄 **Dynamic Response Generation** - Create realistic test scenarios with dynamic data
- 🎯 **Precise Request Matching** - Match requests based on headers, payload, or parameters
- 🔌 **Easy Integration** - Import from Swagger, WSDL, or Postman collections
- 🛠 **Developer-Friendly** - Intuitive UI and comprehensive API support
- 🌐 **Cross-Origin Support** - Built-in CORS support for web applications

## Quick Start

Get up and running in seconds with Docker:

```bash
docker run -p 8080:8080 -p 8085:8085 mockgee/mockgee:latest
```

Access your Mockgee instance:
- 🖥️ UI Dashboard: [http://localhost:8080](http://localhost:8080)
- 🔌 Mock API Endpoint: Port 8085

## Features at a Glance

### Dynamic Mocking
Create varied responses for different test scenarios:
```json
{
    "id": "$$.uuid",
    "timestamp": "$$.timestamp",
    "status": "$$.enum(active,pending,completed)"
}
```

### Request Matching
Match requests with precision:
```javascript
// Path Parameters
/api/users/{userId}

// Query Strings
/api/products?category=electronics&sort=price

// Headers
Authorization: Bearer {token}
```

### Import Support
Bring your existing API definitions:
- OpenAPI/Swagger
- WSDL
- Postman Collections
- CSV/JSON Files

## Getting Started

1. [Installation Guide](getting-started/setup.md) - Set up Mockgee in your environment
2. [Creating Your First Mock](guides/creating-mocks.md) - Learn the basics of creating mocks
3. [Best Practices](guides/best-practices.md) - Tips for effective API mocking

## Use Cases

- 🧪 **Testing & QA**
  - Simulate various API responses
  - Test error scenarios
  - Validate edge cases

- 🔄 **Development**
  - Work offline
  - Parallel development
  - Quick prototyping

- 🤝 **Integration**
  - Third-party API simulation
  - Service virtualization
  - Contract testing

## Community and Support

- 📖 [Documentation](https://docs.mockgee.com)
- 💬 [Community Forum](https://community.mockgee.com)
- 🐛 [Issue Tracker](https://github.com/mockgeelabs/mockgee/issues)

## License

Mockgee is licensed under the [MIT License](LICENSE).

---

<div align="center">

**[Get Started →](getting-started/setup.md)**

</div>