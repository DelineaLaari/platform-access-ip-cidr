# Platform IP/CIDR API

## Overview

The **Platform IP/CIDR API** allows customers to retrieve IP and CIDR information necessary for restricting access to the platform. This API provides data at multiple levels—product, feature, and data boundary—and supports various output formats, making it easier for customers to integrate with their existing systems.

## Features

- Retrieve IP/CIDR data at the product and feature levels.
- Filter results by data boundary (region) and traffic direction (inbound/outbound).
- Support for multiple output formats including:
  - JSON
  - CSV
  - YAML
  - TOML
  - XML
  - Terraform (HCL)
  - Ansible
  - AWS Security Group JSON
  - Cisco ACL
  - PAN-OS
- Pagination support for large datasets.
- Versioning for IP/CIDR data.
- Detailed filtering options.

## API Documentation

The API is built using OpenAPI 3.0. For complete API documentation, including available endpoints and request/response formats, refer to the `api-spec.yaml` file in the repository.


## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (if you're using a Node.js server)
- An API client (Postman, curl, etc.) for testing the API
- Access to the API (API key, if required)

### Installation

1. Clone the repository:

```bash
git clone https://github.com/yourusername/platform-ip-cidr-api.git
```

2. Navigate to the project directory:

```bash
cd platform-ip-cidr-api
```

3. Install dependencies:

```bash
npm install
```

4. (Optional) If you want to run a local server, ensure you have Node.js installed and start the server:

```bash
npm start
```

## Usage
### Example 1 Request
To retrieve IP/CIDR data for all products and features in the US data boundary in CSV format:

```http
GET https://api.example.com/v2/ip-cidr?dataBoundary=US&format=csv
```

### Example 1 Response (CSV Format)
```csv
product,feature,dataBoundary,ip,ports,direction,description
MyProduct,LoginService,US,203.0.113.0/24,443,inbound,"Login service HTTPS access"
AnotherProduct,DataSync,US,198.51.100.0/16,8080,inbound,"Data synchronization service"
```

### Example 2 Request
Retrieve Outbound IPs for a Specific Feature in YAML Format

```http
GET https://api.example.com/v2/ip-cidr?feature=AuditLogs&dataBoundary=APAC&direction=outbound&format=yaml
```
### Example 2 Response (YAML Format)
```yaml
version: "v2.0"
page: 1
pageSize: 20
totalItems: 1
totalPages: 1
lastUpdated: "2024-10-16T12:00:00Z"
data:
  - product: "ThirdProduct"
    feature: "AuditLogs"
    dataBoundary: "APAC"
    ipRanges:
      - ip: "192.0.2.0/24"
        direction: "outbound"
        ports:
          - 80
        description: "Audit logging service HTTP access"
```

### Example 3 Request
Retrieve IP/CIDR Data for All Products in US Data Boundary in IPTables Format

```http
GET https://api.example.com/v2/ip-cidr?dataBoundary=US&format=iptables
```
### Example 3 Response (IPTables Format)
```plaintext
# Generated on 2024-10-16T12:00:00Z
# IP/CIDR rules for the US data boundary

# Allow inbound access for MyProduct LoginService
-A INPUT -s 203.0.113.0/24 -p tcp --dport 443 -j ACCEPT
# Allow inbound access for MyProduct DataSync
-A INPUT -s 198.51.100.0/16 -p tcp --dport 8080 -j ACCEPT
# Allow inbound access for ThirdProduct AuditLogs
-A INPUT -s 192.0.2.0/24 -p tcp --dport 80 -j ACCEPT
```



### Example 4 Request
Retrieve IP/CIDR Data in JSON with Pagination for the US Data Boundary

```http
GET https://api.example.com/v2/ip-cidr?dataBoundary=US&page=2&pageSize=1&format=json

```
### Example 4 Response (JSON Format)

```json
{
  "version": "v2.0",
  "page": 2,
  "pageSize": 1,
  "totalItems": 3,
  "totalPages": 3,
  "lastUpdated": "2024-10-16T12:00:00Z",
  "data": [
    {
      "product": "ThirdProduct",
      "feature": "AuditLogs",
      "dataBoundary": "US",
      "ipRanges": [
        {
          "ip": "192.0.2.0/24",
          "direction": "inbound",
          "ports": [80],
          "description": "Audit logging service HTTP access"
        }
      ]
    }
  ]
}
```



