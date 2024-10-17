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

The API is built using OpenAPI 3.0. For complete API documentation, including available endpoints and request/response formats, refer to the `api.yaml` file in the repository.

### Base URL

https://api.platform.com/v2



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
### Example Request
To retrieve IP/CIDR data for all products and features in the US data boundary in CSV format:

```http
GET https://api.platform.com/v2/ip-cidr?dataBoundary=US&format=csv
```

### Example Response (CSV Format)
```csv
product,feature,dataBoundary,ip,ports,direction,description
MyProduct,LoginService,US,203.0.113.0/24,443,inbound,"Login service HTTPS access"
AnotherProduct,DataSync,US,198.51.100.0/16,8080,inbound,"Data synchronization service"
```










