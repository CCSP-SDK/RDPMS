# RDPMS API Reference

Welcome to the RDPMS API Reference documentation. This page provides detailed information about the various API endpoints available in the RDPMS system.

## Authentication

All API requests require authentication. You must include an API key in the header of each request.

### Example

```http
GET /api/resource HTTP/1.1
Host: api.example.com
Authorization: Bearer YOUR_API_KEY
```

## Endpoints

### 1. Get All Resources

**Endpoint:** `/api/resources`

**Method:** `GET`

**Description:** Retrieves a list of all resources.

**Response:**

```json
[
    {
        "id": 1,
        "name": "Resource 1",
        "description": "Description of Resource 1"
    },
    {
        "id": 2,
        "name": "Resource 2",
        "description": "Description of Resource 2"
    }
]
```

### 2. Get Resource by ID

**Endpoint:** `/api/resources/{id}`

**Method:** `GET`

**Description:** Retrieves a specific resource by its ID.

**Response:**

```json
{
    "id": 1,
    "name": "Resource 1",
    "description": "Description of Resource 1"
}
```

### 3. Create Resource

**Endpoint:** `/api/resources`

**Method:** `POST`

**Description:** Creates a new resource.

**Request Body:**

```json
{
    "name": "New Resource",
    "description": "Description of the new resource"
}
```

**Response:**

```json
{
    "id": 3,
    "name": "New Resource",
    "description": "Description of the new resource"
}
```

### 4. Update Resource

**Endpoint:** `/api/resources/{id}`

**Method:** `PUT`

**Description:** Updates an existing resource.

**Request Body:**

```json
{
    "name": "Updated Resource",
    "description": "Updated description of the resource"
}
```

**Response:**

```json
{
    "id": 1,
    "name": "Updated Resource",
    "description": "Updated description of the resource"
}
```

### 5. Delete Resource

**Endpoint:** `/api/resources/{id}`

**Method:** `DELETE`

**Description:** Deletes a specific resource by its ID.

**Response:**

```json
{
    "message": "Resource deleted successfully"
}
```

## Error Handling

All error responses will include a status code and a message describing the error.

**Example:**

```json
{
    "status": 404,
    "message": "Resource not found"
}
```

For more detailed information on each endpoint, please refer to the specific sections above.
