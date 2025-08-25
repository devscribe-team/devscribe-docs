---
title: Delete Plants 
theme: dark
description: Deletes all plants in your collection
openapi: DELETE https://jsonplaceholder.typicode.com/posts/1
---

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `limit` | integer | Number of plants to return (default: 20, max: 100) |
| `offset` | integer | Number of plants to skip (default: 0) |
| `category` | string | Filter by plant category |

## Example Request

```bash
curl -X GET "https://api.devscribe.com/v1/plants?limit=10&category=succulents" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## Example Response

```json
{
  "data": [
    {
      "id": 1,
      "name": "Snake Plant",
      "category": "succulents",
      "scientific_name": "Sansevieria trifasciata",
      "care_level": "easy",
      "light_requirements": "low to bright indirect",
      "created_at": "2024-01-15T10:30:00Z"
    },
    {
      "id": 2,
      "name": "Fiddle Leaf Fig", 
      "category": "trees",
      "scientific_name": "Ficus lyrata",
      "care_level": "moderate",
      "light_requirements": "bright indirect",
      "created_at": "2024-01-14T09:15:00Z"
    }
  ],
  "pagination": {
    "total": 25,
    "limit": 10,
    "offset": 0,
    "has_more": true
  },
  "success": true
}
```

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique plant identifier |
| `name` | string | Common name of the plant |
| `category` | string | Plant category |
| `scientific_name` | string | Scientific/botanical name |
| `care_level` | string | Difficulty level: easy, moderate, difficult |
| `light_requirements` | string | Light needs description |
| `created_at` | string | ISO 8601 timestamp of creation | 