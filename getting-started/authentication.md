# Authentication

<div align="center">

# 🔐 User Management & Authentication
### Secure Access and User Management in Mockgee

[![Guide Type](https://img.shields.io/badge/Guide-Authentication-success?style=for-the-badge)](https://docs.mockgee.com/getting-started/authentication)
[![Level](https://img.shields.io/badge/Level-Essential-blue?style=for-the-badge)](https://docs.mockgee.com/getting-started/authentication)

</div>

## Overview

Mockgee provides comprehensive user management and authentication features to secure your mock API environment. This guide covers user registration, authentication, and access control.

## Getting Started

### 1. 📝 Sign Up

Create a new Mockgee account:

```
Navigation: Sign Up → Complete Registration Form
```

#### Required Information
- Username/Email
- Password (8+ characters)
- Organization name (optional)

```javascript
// Example Sign Up Request
POST /api/auth/signup
{
  "email": "user@example.com",
  "password": "securePassword123",
  "organization": "My Company"
}
```

### 2. 🔑 Sign In

Access your Mockgee dashboard:

```
Navigation: Sign In → Enter Credentials
```

```javascript
// Example Sign In Request
POST /api/auth/login
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

## User Management

### 1. 👥 User Roles

```javascript
{
  "roles": {
    "admin": {
      "permissions": ["create", "read", "update", "delete", "manage-users"]
    },
    "developer": {
      "permissions": ["create", "read", "update", "delete"]
    },
    "viewer": {
      "permissions": ["read"]
    }
  }
}
```

### 2. 🔄 Role Management

```javascript
// Assign Role
POST /api/users/{userId}/roles
{
  "role": "developer",
  "projects": ["project-1", "project-2"]
}
```

### 3. 👤 User Profile

```javascript
// Update Profile
PUT /api/users/profile
{
  "name": "John Doe",
  "email": "john@example.com",
  "preferences": {
    "theme": "dark",
    "notifications": true
  }
}
```

## Security Features

### 1. 🔒 Password Security

- Minimum 8 characters
- Requires mixed case
- Numbers and symbols
- Regular password updates

### 2. 📱 Two-Factor Authentication

```javascript
{
  "2fa": {
    "enabled": true,
    "methods": [
      "authenticator-app",
      "email"
    ],
    "backup-codes": true
  }
}
```

### 3. 🚫 Access Control

```javascript
{
  "access": {
    "ip-whitelist": ["192.168.1.*"],
    "session-timeout": "4h",
    "max-sessions": 3,
    "rate-limit": {
      "attempts": 5,
      "window": "15m"
    }
  }
}
```

## Team Management

### 1. 👥 Team Creation

```javascript
// Create Team
POST /api/teams
{
  "name": "Development Team",
  "description": "Main development team",
  "members": [
    {
      "email": "dev1@example.com",
      "role": "developer"
    },
    {
      "email": "dev2@example.com",
      "role": "developer"
    }
  ]
}
```

### 2. 🤝 Collaboration Features

```javascript
{
  "collaboration": {
    "shared-projects": true,
    "mock-sharing": true,
    "team-chat": true,
    "activity-feed": true
  }
}
```

## Best Practices

### 1. Account Security
- Use strong passwords
- Enable 2FA
- Regular security audits
- Monitor access logs

### 2. Team Management
- Define clear roles
- Regular access review
- Document permissions
- Implement least privilege

### 3. Authentication
- Secure password storage
- Token-based authentication
- Session management
- Regular token rotation

## Common Operations

### 1. Password Reset
```javascript
// Request Reset
POST /api/auth/reset-password
{
  "email": "user@example.com"
}

// Complete Reset
POST /api/auth/reset-password/complete
{
  "token": "reset-token",
  "newPassword": "newSecurePassword123"
}
```

### 2. Profile Updates
```javascript
// Update Email
PUT /api/users/profile/email
{
  "newEmail": "newemail@example.com",
  "password": "currentPassword123"
}

// Update Password
PUT /api/users/profile/password
{
  "currentPassword": "oldPassword123",
  "newPassword": "newSecurePassword123"
}
```

## Troubleshooting

### Common Issues

1. **Login Issues**
   - Check credentials
   - Verify email confirmation
   - Check account status
   - Reset password if needed

2. **Access Problems**
   - Verify role permissions
   - Check IP restrictions
   - Confirm session validity
   - Review audit logs

## Next Steps

- Set up [Team Access](teams.md)
- Configure [Security Settings](security.md)
- Review [Best Practices](../guides/best-practices.md)

---

<div align="center">

**[← Quick start](getting-started/quickstart)** | **[Features →](../features/README.md)**

</div>