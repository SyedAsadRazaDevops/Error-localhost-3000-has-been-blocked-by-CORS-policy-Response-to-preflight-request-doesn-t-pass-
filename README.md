<H1>Fixing Common Problems with CORS and Lavravel and reactjs (node) project</H1>

# Error-localhost-3000-has-been-blocked-by-CORS-policy-Response-to-preflight-request-doesn-t-pass access control check

# Problem's :

login:1 Access to XMLHttpRequest at  'https://staging.apiapm.digitum.com.sa/login' 
from origin  'http://localhost:3000' has been blocked by CORS policy: 
Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource.

No 'Access-Control-Allow-Origin' header is present on the requested resource—when trying to get data from a REST API

**What is CORS ?**
Many websites have JavaScript functions that make network requests to a server, such as a REST API. The web pages and APIs are often in different domains.
This introduces security issues in that any website can request data from an API. Cross-Origin Resource Sharing (CORS) provides a solution to these issues.
It became a W3C recommendation in 2014. It makes it the responsibility of the web browser to prevent unauthorized access to APIs. 
All modern web browsers enforce CORS. They prevent JavaScript from obtaining data from a server in a domain different than the domain the website was loaded from, 
unless the REST API server gives permission.

there are two ways to resolve this issue by:
- **1#** nginx in site-avalible file
- **2#** laravel cors.php file
>we go with the second one option.
```
<?php

return [

    /*
    |--------------------------------------------------------------------------
    | Cross-Origin Resource Sharing (CORS) Configuration
    |--------------------------------------------------------------------------
    |
    | Here you may configure your settings for cross-origin resource sharing
    | or "CORS". This determines what cross-origin operations may execute
    | in web browsers. You are free to adjust these settings as needed.
    |
    | To learn more: https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
    |
    */

    // 'paths' => ['api/*'],
    'paths' => ['api/*', '*'],

    // 'allowed_methods' => ['*'],
    'allowed_methods' => ['POST', 'GET', 'DELETE', 'PUT', 'PATCH', '*'],

    // 'allowed_origins' => ['*'],
    'allowed_origins' => [
        'http://localhost:3000',
        'http://localhost:8000',
        'http://localhost:8080',
        'https://staging.mydomain.com',
        'https://apimy.test',
        'https://my.test',
    ],

    'allowed_origins_patterns' => [],

    'allowed_headers' => ['*'],
    // 'allowed_headers' => ['X-Custom-Header', 'Upgrade-Insecure-Requests', '*'],
    // 'allowedHeaders' => ['content-type', 'x-csrf-token', 'x-requested-with'],

    'exposed_headers' => [],
    // 'exposed_headers' => ['*'],

    'max_age' => 0,

    // 'supports_credentials' => false,
    'supports_credentials' => true,

];
Collapse

```
write your all local and staging and dev envoirments into the list to allow the request from these URL
```
'http://localhost:3000',
        'http://localhost:8000',
        'http://localhost:8080',
        'https://staging.mydomain.com',
        'https://apimy.test',
        'https://my.test',
```
and turn him true
```
'supports_credentials' => true,
```
allow this path in * formate
```
'paths' => ['api/*', '*'],
``

 
