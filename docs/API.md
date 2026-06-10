# API Reference

This document provides an overview of the primary REST endpoints exposed by the ARC1 Recommendation Engine. All endpoints are versioned under `/api/v1` and return JSON responses.

## Authentication

### Register a new user

`POST /api/v1/auth/register`

Registers a new user with email and password.

**Request body**
```json
{
  "email": "user@example.com",
  "password": "strongpassword",
  "name": "Jane Doe"
}
```

**Response**
```json
{
  "id": "user_uuid",
  "email": "user@example.com",
  "token": "jwt_token"
}
```

### Login

`POST /api/v1/auth/login`

Authenticates a user and returns a JWT access token.

**Request body**
```json
{
  "email": "user@example.com",
  "password": "strongpassword"
}
```

**Response**
```json
{
  "access_token": "jwt_access_token",
  "token_type": "bearer"
}
```

## Content APIs

### Create an item

`POST /api/v1/items`

Creates a new item (e.g., article, product, video) with metadata.

**Request body**
```json
{
  "title": "Example Item",
  "description": "A short description",
  "tags": ["sample", "demo"]
}
```

**Response**
```json
{
  "id": "item_uuid",
  "title": "Example Item",
  "created_at": "2026-06-10T12:00:00Z"
}
```

### Retrieve an item

`GET /api/v1/items/{item_id}`

Returns the item with the given `item_id`.

## Ratings APIs

### Add or update a rating

`POST /api/v1/ratings`

Rates an item by a user. If a rating already exists, it will be updated.

**Request body**
```json
{
  "user_id": "user_uuid",
  "item_id": "item_uuid",
  "rating": 4.5
}
```

## Recommendation Endpoint

### Get recommendations for a user

`GET /api/v1/recommendations/{user_id}`

Returns a ranked list of recommended items for the user. Accepts optional query parameters such as `limit` and `exclude_rated`.

**Example**
```
GET /api/v1/recommendations/12345?limit=10&exclude_rated=true
```

**Response**
```json
{
  "user_id": "12345",
  "recommendations": [
    {
      "item_id": "item_1",
      "score": 0.95
    },
    {
      "item_id": "item_2",
      "score": 0.87
    }
  ]
}
```

## ReviewOps

For details on the human-in-the-loop review process, see `REVIEWOPS.md` in this directory.
