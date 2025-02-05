# Importers

<div align="center">

# 📥 API Importers
### Streamline Mock Creation with Existing API Specifications

[![Feature Status](https://img.shields.io/badge/Status-Stable-success?style=for-the-badge)](https://docs.mockgee.com/features/importer)
[![Use Case](https://img.shields.io/badge/Use%20Case-Integration-blue?style=for-the-badge)](https://docs.mockgee.com/features/importer)

</div>

## Overview

Mockgee's Import feature accelerates your mock API development by seamlessly integrating with commonly used API specification formats. Import your existing API definitions and instantly create mock endpoints ready for testing.

## Supported Formats

### 📋 OpenAPI (Swagger)
- OpenAPI 2.0 (Swagger)
- OpenAPI 3.0
- JSON and YAML formats

### 🔄 SOAP/WSDL
- WSDL 1.1 and 2.0
- XML Schema support
- Complex type definitions

### 📦 Postman
- Collection v2.0+
- Environment variables
- Request examples

### 📊 Data Formats
- CSV files with headers
- JSON data structures
- Nested object support

## Import Process

### 1. Access the Importer
```
Mock → Importer → Select Format
```

### 2. Choose Import Method
- File Upload
- URL Import
- Copy/Paste Content

### 3. Configuration Options
- Endpoint prefix customization
- Response example selection
- Header mapping
- Authentication settings

## Step-by-Step Guide

### OpenAPI/Swagger Import

1. **Prepare Your Specification**
   ```yaml
   openapi: 3.0.0
   info:
     title: Sample API
     version: 1.0.0
   paths:
     /users:
       get:
         responses:
           '200':
             description: Success
             content:
               application/json:
                 example:
                   users:
                     - id: 1
                       name: "John Doe"
   ```

2. **Import Process**
   - Navigate to Importer
   - Select OpenAPI format
   - Upload or paste specification
   - Configure options
   - Start import

3. **Review & Customize**
   - Verify endpoints
   - Adjust response examples
   - Configure matchers
   - Set dynamic data

### WSDL Import

1. **Prepare WSDL File**
   ```xml
   <?xml version="1.0"?>
   <definitions name="UserService"
                targetNamespace="http://example.com/users">
     <message name="getUserRequest">
       <part name="userId" type="xsd:string"/>
     </message>
     <!-- Additional WSDL content -->
   </definitions>
   ```

2. **Import Steps**
   - Choose WSDL import
   - Upload WSDL file
   - Map operations
   - Configure responses

3. **Post-Import Setup**
   - Review generated endpoints
   - Customize response data
   - Set up fault scenarios

### Postman Collection Import

1. **Export Collection**
   - Export from Postman
   - Include examples
   - Save environment variables

2. **Import Process**
   - Select Postman format
   - Upload collection
   - Configure variables
   - Map responses

3. **Finalize Setup**
   - Verify request mapping
   - Set up dynamic responses
   - Configure authentication

## Advanced Features

### 🔄 Bulk Import
Import multiple specifications:
```bash
POST /api/v1/import/bulk
Content-Type: multipart/form-data

files: [swagger.yaml, api.wsdl, collection.json]
```

### 🔍 Smart Detection
Automatic format detection and parsing:
```javascript
{
    "autoDetect": true,
    "fallbackFormat": "openapi",
    "validateSchema": true
}
```

### 🔄 Sync Updates
Keep mocks in sync with specification:
```javascript
{
    "syncMode": "update",
    "preserveCustomizations": true,
    "updateFrequency": "daily"
}
```

## Best Practices

### 1. Preparation
- Validate specifications before import
- Clean up unused definitions
- Document custom requirements

### 2. Import Process
- Start with a test import
- Review generated endpoints
- Verify response formats
- Check authentication setup

### 3. Post-Import
- Customize response data
- Set up dynamic elements
- Configure request matchers
- Test all endpoints

## Troubleshooting

### Common Issues

1. **Import Failures**
   - Verify file format
   - Check specification validity
   - Review error messages

2. **Missing Endpoints**
   - Check specification completeness
   - Verify path configurations
   - Review import logs

3. **Response Mismatch**
   - Compare with original spec
   - Check content type mapping
   - Verify example data

## Example Configurations

### OpenAPI Import Config
```json
{
    "format": "openapi",
    "options": {
        "baseUrl": "/api/v1",
        "headers": {
            "Content-Type": "application/json"
        },
        "authentication": {
            "type": "bearer",
            "token": "sample-token"
        }
    }
}
```

### WSDL Import Config
```json
{
    "format": "wsdl",
    "options": {
        "endpoint": "/soap/users",
        "namespace": "http://example.com/users",
        "generateFaults": true
    }
}
```

## Next Steps

- Explore [Dynamic Mock](dynamic-mock.md) features
- Learn about [Request Matcher](request-matcher.md)
- Check [Best Practices](../guides/best-practices.md)

---

<div align="center">

**[← Fake Data](fake-data.md)** | **[CORS Support →](cors.md)**

</div>