# Links

## Link Retrieval

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/link" summary="Get link destination by slug" %}
{% swagger-description %}
Retrieves the destination of link by its slug (unauthed).
{% endswagger-description %}

{% swagger-parameter in="query" name="slug" required="true" %}
The slug of the link
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Link successfully created" %}
```javascript
{
    "success": true,
    "result": {
        "destination": "https://github.com/Lynx-Shortener/Docs",
    }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid slug" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/link" summary="Get full link by slug" %}
{% swagger-description %}
Retrieves the full link information by its slug.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-parameter in="query" name="id" required="true" %}
The slug of the link
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Link successfully retrieved" %}
```javascript
{
    "success": true,
    "result": {
        "id": "6023f6ec-4283-4ece-a4de-5acbb30357d9",
        "slug": "qKK0AR34",
        "destination": "https://github.com/Lynx-Shortener/Docs",
        "author": "be8881ce-af01-433b-a675-fe02e8a48a88",
        "creationDate": "2023-05-26T13:21:31.803Z",
        "modifiedDate": "2023-05-26T13:21:31.803Z",
        "visits": 0
    }
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Invalid slug" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="get" path="/link/list" summary="Retrieve paginated links" %}
{% swagger-description %}
Retrieve a list of paginated links that the user has permission to see. An admin can see all links but a standard user can only see their own.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pagesize" required="true" %}
Items to return in a page, up to 100.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="page" required="true" %}
The current page to return, 0-base indexed.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="search" %}
Value to search slug and destination by.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sortType" type="Intege" required="true" %}
Order to sort by. -1 or 1.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sortField" required="true" %}
Field to sort by. id, slug, destination, author, creationDate, modifiedDate or visits.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Links successfully retrieved" %}
```javascript
{
    "success": true,
    "result": {
        "remaining": 0,
        "links": [
            {
                "id": "f03eb6f5-d9ce-42ab-9506-f0e438304308",
                "slug": "author",
                "destination": "https://jackbailey.dev",
                "author": "be8881ce-af01-433b-a675-fe02e8a48a88",
                "creationDate": "2023-05-26T13:47:54.168Z",
                "modifiedDate": "2023-05-26T13:47:54.168Z",
                "visits": 0,
                "account": "demo"
            },
            {
                "id": "2fabe8c4-374e-458f-b8ad-9ef72badb2b3",
                "slug": "website",
                "destination": "https://getlynx.dev",
                "author": "be8881ce-af01-433b-a675-fe02e8a48a88",
                "creationDate": "2023-05-26T13:47:32.752Z",
                "modifiedDate": "2023-05-26T13:47:40.649Z",
                "visits": 1,
                "account": "demo"
            },
            {
                "id": "e845ff19-c3c3-4cd0-8e54-f932809a3126",
                "slug": "website-source",
                "destination": "https://github.com/Lynx-Shortener/Website",
                "author": "be8881ce-af01-433b-a675-fe02e8a48a88",
                "creationDate": "2023-05-26T13:47:23.016Z",
                "modifiedDate": "2023-05-26T13:47:23.016Z",
                "visits": 0,
                "account": "demo"
            }
        ]
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

## Link Management

{% swagger baseUrl="https://demo.getlynx.dev/api" method="post" path="/link" summary="Create link" %}
{% swagger-description %}
Creates a a link.
{% endswagger-description %}

{% swagger-parameter in="body" name="slug" required="true" type="string" %}
The slug of the new link
{% endswagger-parameter %}

{% swagger-parameter in="body" name="destination" required="true" type="string" %}
The destination of the new link
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Link successfully created" %}
```javascript
{
    "success": true,
    "result": {
        "id": "6023f6ec-4283-4ece-a4de-5acbb30357d9",
        "slug": "qKK0AR34",
        "destination": "https://github.com/Lynx-Shortener/Docs",
        "author": "be8881ce-af01-433b-a675-fe02e8a48a88",
        "creationDate": "2023-05-26T13:21:31.803Z",
        "modifiedDate": "2023-05-26T13:21:31.803Z",
        "visits": 0,
        "account": "demo"
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Permission denied" %}

{% endswagger-response %}

{% swagger-response status="409: Conflict" description="A link with that slug/destination already exists" %}
Destination conflict only occurs when URL_ONLY_UNIQUE is set
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Destination doesn't match URL regex" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="patch" path="/link" summary="Update link" %}
{% swagger-description %}
Updates a a link.
{% endswagger-description %}

{% swagger-parameter in="body" name="id" required="true" %}
The id of the link
{% endswagger-parameter %}

{% swagger-parameter in="body" name="slug" required="true" type="string" %}
The slug of the link to set
{% endswagger-parameter %}

{% swagger-parameter in="body" name="destination" required="true" type="string" %}
The destination of the link to set
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Link successfully updated" %}
```javascript
{
    "success": true,
    "result": {
        "id": "6023f6ec-4283-4ece-a4de-5acbb30357d9",
        "slug": "qKK0AR34",
        "destination": "https://github.com/Lynx-Shortener/Website",
        "author": "be8881ce-af01-433b-a675-fe02e8a48a88",
        "creationDate": "2023-05-26T13:21:31.803Z",
        "modifiedDate": "2023-05-26T13:28:21.642Z",
        "visits": 0,
        "account": "demo"
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Permission denied" %}

{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="You do not have permissions to edit this link" %}

{% endswagger-response %}

{% swagger-response status="404: Not Found" description="A link with that id does not exist" %}

{% endswagger-response %}

{% swagger-response status="409: Conflict" description="A link with that slug/destination already exists" %}
Destination conflict only occurs when URL_ONLY_UNIQUE is set
{% endswagger-response %}

{% swagger-response status="422: Unprocessable Entity" description="Invalid slug/destination format" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://demo.getlynx.dev/api" method="delete" path="/link" summary="Delete link" %}
{% swagger-description %}
Deletes a a link.
{% endswagger-description %}

{% swagger-parameter in="body" name="ids" required="true" type="Array" %}
The id of links to remove
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" required="false" %}
Your API key
{% endswagger-parameter %}

{% swagger-parameter in="cookie" name="token" %}
Your JWT Session
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Link successfully deleted" %}
```javascript
{
    "success": true
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Permission denied" %}

{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="You do not have the permissions to delete some of or all of the selected links. No links were deleted" %}

{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}

{% endswagger-response %}
{% endswagger %}
