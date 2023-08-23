---
description: >-
  All endpoints require you to be an admin or the owner and cannot be used with
  an API token.
---

# Users

## Authentication

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/user/list" summary="Get Users" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" name="token" required="true" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Users successfully listed" %}
```javascript
{
    "success": true,
    "result": [
        {
            "id": "e11fb6ed-3186-473c-87e9-a8d7c71b64e2",
            "username": "owner",
            "email": "admin@getlynx.dev",
            "role": "owner",
            "secret": "KVp6rz8P95VNa6oU0bDMWNZppCpXE5u9"
        },
        {
            "id": "3fbcf68c-84a3-48c7-8e35-a57b1621a5be",
            "username": "user",
            "email": "user@getlynx.dev",
            "role": "standard",
            "secret": null
        }
    ]
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}

{% endswagger-response %}

{% swagger-response status="412: Precondition Failed" description="User is not the owner or an admin" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/user" summary="Create User" %}
{% swagger-description %}
Works, even when registration is disabled.
{% endswagger-description %}

{% swagger-parameter in="body" name="verification.token" %}
Your 2FA Token if enabled
{% endswagger-parameter %}

{% swagger-parameter in="body" name="verification.password" %}
Your password if 2FA not enabled
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user.username" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="user.password" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="user.email" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="user.role" required="true" %}
If owner, this can be "admin" or "standard".

\


If "admin", this field can only be "standard".
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successfully created account" %}
```javascript
{
    "success": true,
    "result": "Account created",
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid field(s)" %}
```javascript
{
  "success": false,
  "message": "Invalid field(s)",
  "details": {
      "invalid": {
          "email": false,
          "username": false,
          "password": true,
      },
  },  
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Field(s) are already used" %}
```javascript
{
  "success": false,
  "message": "Field(s) are already used",
  "details": {
      "exists": {
          "email": true,
          "username": true,
          "password": false,
      },
  },  
}
```


{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Demo mode is enabled, users cannot be created" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/user/role" summary="Update user role" %}
{% swagger-description %}
Requires you to be the owner, if the role is set to owner, your account will be demoted to an admin.
{% endswagger-description %}

{% swagger-parameter in="cookie" name="token" required="true" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-parameter in="body" name="verification.token" %}
Your 2FA Token if enabled
{% endswagger-parameter %}

{% swagger-parameter in="body" name="verification.password" %}
Your password if 2FA not enabled
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user.role" required="true" %}
"owner", "admin" or "standard" 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user.userID" %}
User ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Account role successfully updated" %}
```javascript
{
    "success": true,
    "result": {
        "user": {
            "id": "e11fb6ed-3186-473c-87e9-a8d7c71b64e2",
            "username": "owner",
            "email": "admin@getlynx.dev",
            "role": "owner",
            "secret": "KVp6rz8P95VNa6oU0bDMWNZppCpXE5u9"
        }
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="A user object is required" %}

{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Invalid User ID" %}

{% endswagger-response %}

{% swagger-response status="417: Expectation Failed" description="Invalid role" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="delete" path="/user" summary="Delete User" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" name="token" required="true" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-parameter in="body" name="verification.token" %}
Your 2FA Token if enabled
{% endswagger-parameter %}

{% swagger-parameter in="body" name="verification.password" %}
Your password if 2FA not enabled
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user.id" required="true" %}
User ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Account successfully deleted" %}
```javascript
{
    "success": true,
    "message": "Deleted account!",
}
```
{% endswagger-response %}
{% endswagger %}

#### Manual Promotion

If you accidentally promote the wrong user or otherwise would like to make yourself an admin again, run these commands:

Connect to your database and enter your password:

```bash
mongosh --port 27017 --username user --authenticationDatabase admin
```

Switch to the lynx database:

```mongodb
use shortener
```

Demote the old owner to an admin

{% code fullWidth="false" %}
```mongodb
db.accounts.findOneAndUpdate({ role: "owner" },{ $set:{ role: "admin" } })
```
{% endcode %}

Promote yourself to owner

```mongodb
db.accounts.findOneAndUpdate({ username: "YOUR USERNAME" },{ $set:{ "role": "owner" } })
```
