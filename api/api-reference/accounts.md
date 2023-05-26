# Accounts

## Authentication

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/auth/me" summary="Get Account" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Account successfully returned" %}
```javascript
{
    "success": true,
    "result":{
        "id":"be8881ce-af01-433b-a675-fe02e8a48a88",
        "username":"demo",
        "email":"demo@example.com",
        "role":"standard",
        "secret":"uihJEIwC0jjGIF0BhZnY7xI90jN664La",
        "totp": false,
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/auth/login" summary="Log In" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="username" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" %}
2FA Token
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successfully logged in" %}
```javascript
// Returns set-cookie header set to JWT Session under "token"
{
    "success": true,
    "message": "Successfully logged in!",
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Invalid username or password" %}

{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="2FA token required" %}
```javascript
{
    "success": false,
    "message": "2FA token required",
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/auth/register" summary="Register" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="username" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" required="true" %}

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

{% swagger-response status="412: Precondition Failed" description="Registration is not enabled" %}
Occurs when at least 1 account exists and ENABLE_REGISTRATION is set to false
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="delete" path="/auth/me" summary="Log Out" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="cookie" name="token" required="true" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Account successfully logged out" %}
```javascript
// Cookie token is cleared
{
    "success": true,
    "message": "Successfully logged out",
}
```
{% endswagger-response %}
{% endswagger %}

## Two-Factor Authentication (2FA)

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/auth/totp" summary="Get new TOTP token" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="New TOTP token generated" %}
```javascript
{
    "success": true,
    "message": "TOTP secret successfully generated",
    "result":{
        "secret": "H6NYN2R23UB6KGAC3O6TARUVN773MBWT",
        "uri": "otpauth://totp/Lynx:admin?issuer=Lynx&secret=H6NYN2R23UB6KGAC3O6TARUVN773MBWT&algorithm=SHA1&digits=6&period=30"
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}

{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Enabling 2FA is not supported in demo mode." %}

{% endswagger-response %}

{% swagger-response status="412: Precondition Failed" description="2FA already enabled" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/auth/totp" summary="Enable 2FA" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" required="true" %}
2FA Token
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="2FA successfully enabled" %}
```javascript
{
    "success": true,
    "message": "2FA successfully enabled",
    "result":{
        "backupCodes": ["57E5ht9zD1d3", "6bllbg1122Qc", "76A7n7AHEm0r", "6VL2z2W151L5", "fQxPJJ6AYTu2", "S2uZ7A12k551"],
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}

{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Enabling 2FA is not supported in demo mode." %}

{% endswagger-response %}

{% swagger-response status="412: Precondition Failed" description="2FA process hasn't been started" %}

{% endswagger-response %}

{% swagger-response status="412: Precondition Failed" description="2FA already enabled, no need to verify" %}

{% endswagger-response %}

{% swagger-response status="412: Precondition Failed" description="Invalid token format" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="delete" path="/auth/totp" summary="Disable 2FA" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" %}
2FA Token
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="2FA successfully disabled" %}
```javascript
{
    "success": true,
    "message": "2FA has been successfully disabled",
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}

{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Expired or invalid TOTP token" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

### Account Recovery

{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/auth/totp/recover" summary="Recover Account" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="username" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-parameter in="body" name="backupCode" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="2FA has been disabled and you have been logged in" %}
```javascript
// Returns set-cookie header set to JWT Session under "token"
{
    "success": true,
    "message": "2FA has been disabled and you have been logged in",
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Invalid username or password" %}

{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Invalid backup code" %}

{% endswagger-response %}

{% swagger-response status="412: Precondition Failed" description="2FA is not enabled" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

#### Manual Recovery

If you didn't save your backup codes you will need to run the following commands in your mongodb container/instance

Connect to your database and enter your password:

```bash
mongosh --port 27017 --username user --authenticationDatabase admin
```

Switch to the lynx database:

```mongodb
use shortener
```

Disable 2FA for your account's username:

```mongodb
db.accounts.findOneAndUpdate({ username: "user2" },{ $set:{ "totp.enabled":false } })
```





## Account Information Management

{% swagger baseUrl="https://demo.getlynx.dev/api" method="patch" path="/auth/email" summary="Update Email" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="newEmail" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" %}
2FA Token (If Enabled)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successfully updated email" %}
```javascript
{
    "success": true,
    "result": "Email successfully updated",
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid password" %}

{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Updating of credentials is not enabled in demo mode." %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="patch" path="/auth/password" summary="Update Password" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="password" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="newPassword" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" %}
2FA Token (If Enabled)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successfully updated password" %}
```javascript
{
    "success": true,
    "result": "Password successfully updated",
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid password" %}

{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Updating of credentials is not enabled in demo mode." %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="patch" path="/auth/username" summary="Update Username" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="newUsername" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" %}
2FA Token (If Enabled)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successfully updated username" %}
```javascript
{
    "success": true,
    "result": "Username successfully updated",
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid password" %}

{% endswagger-response %}

{% swagger-response status="406: Not Acceptable" description="Updating of credentials is not enabled in demo mode." %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

