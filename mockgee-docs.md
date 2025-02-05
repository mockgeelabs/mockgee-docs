# Mockgee Documentation

> Mockgee - The Leading API Mocking Solution for Modern Development

## Getting Started

### Quick Installation

Get started with Mockgee using Docker:

```bash
docker run -p 8080:8080 -p 8085:8085 mockgee/mockgee:latest
```

For Ubuntu users, use our single-line installation:

```bash
curl -fsSL https://raw.githubusercontent.com/mockgeelabs/mockgee-install/main/mockgee.sh -o mockgee.sh && chmod +x mockgee.sh && ./mockgee.sh install
```

### Accessing Mockgee
- Web UI: http://localhost:8080
- Mock API Endpoint: Port 8085

## Core Features

### 1. Dynamic Mocking
- Configure multiple mock responses for specific endpoints
- Runtime response selection based on request criteria
- Perfect for testing various scenarios including error cases
- Enhanced test coverage capabilities

### 2. Request Matching
Mockgee provides powerful request matching capabilities:

#### Path Parameters
- Support for dynamic path parameters
- Example: `/api/user/{userId}` with different responses for different IDs

#### Query String Handling
- Static query string matching
- Dynamic query string support using wildcards
- Example: `https://example.com/api/users?*` matches any query parameters

#### Header Matching
- Response selection based on request headers
- Flexible header-based routing

#### Payload Matching Options
- Full payload matching
- Specific field matching
- Field ignoring capabilities
- Complete payload ignore option

### 3. Fake Data Generation
Generate dynamic mock data using simple syntax:

```json
{
    "ID": "$$.uuid",
    "name": "$$.name",
    "isEmployee": "$$.boolean",
    "phoneNumber": "$$.int(9)"
}
```

Supported Data Types:
- uuid: Generates unique identifiers
- ip: Creates valid IP addresses
- name: Generates random names
- int/ints: Numeric values
- float: Decimal numbers
- timestamp: Current timestamps
- boolean: True/false values
- enum: Custom value sets

### 4. Import Capabilities
Supported formats:
- OpenAPI (Swagger)
- WSDL
- Postman Collections
- CSV Files
- JSON Files

### 5. CORS Support
Built-in Cross-Origin Resource Sharing support for seamless cross-domain testing.

### 6. Proxy Mode
- Redirect requests to actual applications
- Fallback capability when no mock matches
- Perfect for hybrid testing scenarios

## Creating Mocks

### Method 1: Import Existing Specifications
1. Navigate to "Mock" → "Importer"
2. Select or drag your specification file
3. Click "Import"
4. Customize generated mocks as needed

### Method 2: Manual Creation
1. Go to "Mock" → "Add"
2. Configure:
   - HTTP method
   - Endpoint path
   - Response headers
   - Response body
   - Status codes
3. Set up request matchers
4. Configure advanced settings (mapping, delays)

### Method 3: RESTful API Integration
- Programmatic mock creation
- CI/CD pipeline integration
- Authentication support

## Default Response Configuration
1. Navigate to Mock folder
2. Access API | Services
3. Select your project
4. Configure default responses for unmatched requests

## Best Practices
- Use dynamic mocks for complex scenarios
- Leverage request matchers for precise control
- Implement fake data for realistic testing
- Utilize proxy mode for hybrid testing approaches
- Configure appropriate CORS settings for web applications

## Troubleshooting
- Verify correct ports (8080 for UI, 8085 for API)
- Check request matcher configurations
- Validate import file formats
- Review proxy settings if using proxy mode