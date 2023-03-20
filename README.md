# Tradeful test

## Overview

To install app: 

1. clone repo
2. run `composer install `
3. run `./vendor/bin/sail up`
4. run `./vendor/bin/sail composer install`
5. run `./vendor/bin/sail artisan migrate --seed`
6. run `./vendor/bin/sail npm install && ./vendor/bin/sail npm run dev`
7. open browser to `localhost:85` (or whichever port you configured in the .env file)



## Create a token

Send a POST request to the `api/sanctum/token` endpoint. Define the Content-Type as application/json.
Here is an example using the user created from the database seeder UserTableSeeder:

```POST /api/sanctum/token HTTP/1.1
Content-Type: application/json
Host: 127.0.0.1:8000
Connection: close
User-Agent: RapidAPI/4.1.3 (Macintosh; OS X/12.1.0) GCDHTTPRequest
Content-Length: 88

{"password":"admin","email":"hemham914@gmail.com","device_name":"Some Mobile Device"}
```

### Curl command

```
curl -X "POST" "http://127.0.0.1:8000/api/sanctum/token" \
     -H 'Content-Type: application/json' \
     -d $'{
  "email": "hemham914@gmail.com",
  "device_name": "Some Mobile Device",
  "password": "admin"
}'
```

If authentication was successful, it will return a bearer token.

```
HTTP/1.1 200 OK
Host: 127.0.0.1:8000
Date: Sat, 18 Mar 2023 02:39:58 GMT
Connection: close
X-Powered-By: PHP/8.1.8
Content-Type: text/html; charset=UTF-8
Cache-Control: no-cache, private
Date: Sat, 18 Mar 2023 02:39:58 GMT
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 57
Access-Control-Allow-Origin: *

1|vJh6x0LCXhe1FiuOyWeLoq2Akk7tjs6MY****zlL9Uvp
```

## Using the Token

**All subsequent requests to the API can be made by adding an `Authorization` header and specifying its value as `Bearer {token}`.**

### Get all blirps

```
curl "http://127.0.0.1:8000/api/blirps" \
     -H 'Content-Type: application/json' \
     -H 'Authorization: Bearer {YOUR BEARER TOKEN}'
```

### Get single book

```
curl "http://127.0.0.1:8000/api/blirps/1" \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {YOUR BEARER TOKEN}'
```

### Create book

```
curl -X "POST" "http://127.0.0.1:8000/api/blirps" \
     -H 'Content-Type: application/json' \
     -H 'Authorization: Bearer {YOUR BEARER TOKEN}' \
     -d $'{
  "author": "jesse griffin",
  "title": "ddd",
  "price": "49.99",
  "editor": "Apress"
}'
```

### Update book

```
curl "http://127.0.0.1:8000/api/blirps/20" \
-X PUT
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {YOUR BEARER TOKEN}' \
-d  '{"title":"Fuber","price":"999.99","author":"Some guy","editor":"Editor McGee"}'
```


## Pagination

``` 
curl "http://127.0.0.1:8000/api/blirps/1?page=2" \
     -H 'Content-Type: application/json' \
     -H 'Authorization: Bearer {YOUR BEARER TOKEN}'
```
