# GitHub Profile Shop - API Documentation

## Base URL
```
http://localhost:3000/api/github
```

## Rate Limiting
- **Standard endpoints**: 100 requests per 15 minutes per IP
- **Strict endpoints** (trending, cache): 30 requests per 15 minutes per IP

## Response Format

### Success Response
```json
{
  "success": true,
  "data": { ... }
}
```

### Error Response
```json
{
  "success": false,
  "error": "Error message",
  "message": "Detailed error description"
}
```

---

## Endpoints

### 1. Fetch Users
Retrieve a paginated list of GitHub users.

**Endpoint**: `GET /api/github/users`

**Query Parameters**:
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `since` | number | 0 | Starting user ID for pagination |
| `per_page` | number | 30 | Number of users to fetch (max: 100) |

**Example Request**:
```bash
curl "http://localhost:3000/api/github/users?since=0&per_page=15"
```

**Example Response**:
```json
{
  "success": true,
  "data": [
    {
      "login": "octocat",
      "id": 1,
      "avatar_url": "https://avatars.githubusercontent.com/u/1?v=4",
      "type": "User",
      "name": "The Octocat",
      "company": "@github",
      "location": "San Francisco",
      "public_repos": 8,
      "followers": 100000,
      "following": 0
    }
  ]
}
```

---

### 2. Get User Details
Fetch detailed information about a specific user.

**Endpoint**: `GET /api/github/user/:username`

**Path Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| `username` | string | GitHub username |

**Example Request**:
```bash
curl "http://localhost:3000/api/github/user/octocat"
```

**Example Response**:
```json
{
  "success": true,
  "data": {
    "login": "octocat",
    "id": 1,
    "name": "The Octocat",
    "avatar_url": "https://avatars.githubusercontent.com/u/1?v=4",
    "bio": "How people build software",
    "company": "@github",
    "location": "San Francisco",
    "email": null,
    "blog": "https://github.blog",
    "twitter_username": null,
    "public_repos": 8,
    "public_gists": 8,
    "followers": 100000,
    "following": 0,
    "created_at": "2011-01-25T18:44:36Z",
    "updated_at": "2024-01-10T12:00:00Z",
    "hireable": true
  }
}
```

---

### 3. Search Users
Search for GitHub users by query string.

**Endpoint**: `GET /api/github/search`

**Query Parameters**:
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `q` | string | required | Search query |
| `page` | number | 1 | Page number |

**Example Request**:
```bash
curl "http://localhost:3000/api/github/search?q=john&page=1"
```

**Example Response**:
```json
{
  "success": true,
  "data": {
    "total_count": 1000,
    "incomplete_results": false,
    "items": [
      {
        "login": "john",
        "id": 123,
        "avatar_url": "https://avatars.githubusercontent.com/u/123?v=4",
        "type": "User"
      }
    ]
  }
}
```

---

### 4. Get User Repositories
Fetch repositories for a specific user.

**Endpoint**: `GET /api/github/user/:username/repos`

**Path Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| `username` | string | GitHub username |

**Query Parameters**:
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `sort` | string | updated | Sort by: updated, created, pushed, full_name |
| `per_page` | number | 10 | Number of repos to fetch |

**Example Request**:
```bash
curl "http://localhost:3000/api/github/user/octocat/repos?sort=updated&per_page=5"
```

**Example Response**:
```json
{
  "success": true,
  "data": [
    {
      "name": "Hello-World",
      "full_name": "octocat/Hello-World",
      "description": "My first repository on GitHub!",
      "html_url": "https://github.com/octocat/Hello-World",
      "language": "JavaScript",
      "stargazers_count": 1000,
      "forks_count": 500,
      "updated_at": "2024-01-10T12:00:00Z"
    }
  ]
}
```

---

### 5. Get User Followers
Fetch followers for a specific user.

**Endpoint**: `GET /api/github/user/:username/followers`

**Path Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| `username` | string | GitHub username |

**Example Request**:
```bash
curl "http://localhost:3000/api/github/user/octocat/followers"
```

**Example Response**:
```json
{
  "success": true,
  "data": [
    {
      "login": "follower1",
      "id": 456,
      "avatar_url": "https://avatars.githubusercontent.com/u/456?v=4",
      "type": "User"
    }
  ]
}
```

---

### 6. Get User Following
Fetch users that a specific user follows.

**Endpoint**: `GET /api/github/user/:username/following`

**Path Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| `username` | string | GitHub username |

**Example Request**:
```bash
curl "http://localhost:3000/api/github/user/octocat/following"
```

---

### 7. Get User Gists
Fetch gists for a specific user.

**Endpoint**: `GET /api/github/user/:username/gists`

**Path Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| `username` | string | GitHub username |

**Example Request**:
```bash
curl "http://localhost:3000/api/github/user/octocat/gists"
```

**Example Response**:
```json
{
  "success": true,
  "data": [
    {
      "id": "gist123",
      "description": "My code snippet",
      "html_url": "https://gist.github.com/octocat/gist123",
      "files": { ... },
      "created_at": "2024-01-01T00:00:00Z"
    }
  ]
}
```

---

### 8. Get Trending Repositories
Fetch trending repositories from GitHub.

**Endpoint**: `GET /api/github/trending`

**Query Parameters**:
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `language` | string | javascript | Programming language |
| `since` | string | weekly | Time range: daily, weekly, monthly |

**Example Request**:
```bash
curl "http://localhost:3000/api/github/trending?language=javascript&since=weekly"
```

---

### 9. Health Check
Check if the server is running.

**Endpoint**: `GET /api/health`

**Example Request**:
```bash
curl "http://localhost:3000/api/health"
```

**Example Response**:
```json
{
  "status": "OK",
  "timestamp": "2024-01-10T12:00:00Z"
}
```

---

### 10. Clear Cache
Clear the server-side cache.

**Endpoint**: `DELETE /api/github/cache`

**Query Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| `key` | string | Optional specific cache key to clear |

**Example Request**:
```bash
# Clear all cache
curl -X DELETE "http://localhost:3000/api/github/cache"

# Clear specific key
curl -X DELETE "http://localhost:3000/api/github/cache?key=users_0_30"
```

---

## Error Codes

| Status Code | Description |
|-------------|-------------|
| 200 | Success |
| 400 | Bad Request - Invalid parameters |
| 404 | Not Found - User/resource not found |
| 429 | Too Many Requests - Rate limit exceeded |
| 500 | Internal Server Error |
| 503 | Service Unavailable - GitHub API down |

---

## Rate Limit Headers

Response headers include rate limit information:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1704888000
```

---

## Caching

- Default TTL: 10 minutes (600 seconds)
- Cache is automatically invalidated on expiry
- Use `/api/github/cache` DELETE to manually clear

---

## Authentication

### Without Token
- 60 requests per hour to GitHub API
- Suitable for development/testing

### With Token
Add to `server/.env`:
```env
GITHUB_TOKEN=ghp_your_token_here
```
- 5000 requests per hour to GitHub API
- Recommended for production

Get your token: https://github.com/settings/tokens

---

## Example Integration

### JavaScript Fetch
```javascript
// Get user profile
const response = await fetch('/api/github/user/octocat');
const { success, data } = await response.json();

if (success) {
  console.log(data.name); // "The Octocat"
}
```

### cURL
```bash
# Get users
curl http://localhost:3000/api/github/users

# Search
curl "http://localhost:3000/api/github/search?q=react"

# Get specific user
curl http://localhost:3000/api/github/user/facebook
```
