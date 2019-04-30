
# Postman With JavaScript |REST API Testing|Best for Beginners

**REST API** - **Re**presentational **S**tate **T**ransfer API

**Postman sandbox** is the JS engine within Postman tool.

Pre-req > Request > Response > Tests

## Install and run JSON Server

npm install -g json-server

$ json-server --watch db.json

## Basic GET, POST, PUT and DELETE request

```json
GET http://localhost:3000/posts

GET http://localhost:3000/posts/1

POST http://localhost:3000/posts
    body: { "id": 2, "title": "2-json-server", "author": "2-typicode" }

PUT http://localhost:3000/posts/2
    body: { "id": 2, "title": "2-json-server-updated", "author": "2-typicode-updated" }

DELETE http://localhost:3000/posts/2
```

## Add verification: Status code, response body and time

```json
GET http://localhost:3000/posts/1

Tests:
    tests["Verify status code"] = responseCode.code === 200;
    tests["Verify response body"] = responseBody.has("json-server");
    tests["Verify response time is less than 300ms"] = responseTime <= 300;

Result:
    PASS Verify status code
    PASS Verify response body
    PASS Verify response time is less than 300ms
```

## E2E Test

1. Create a new record.

   ```json
   POST http://localhost:3000/posts
   Request body: { "id": 2, "title": "2-json-server", "author": "2-typicode" }

   Response status code: "201 Created"
   Response body: { "id": 2, "title": "2-json-server", "author": "2-typicode" }
    ```

2. Verify record data.

   ```json
   GET http://localhost:3000/posts/2

   Response status code: "200 OK"
   Response body: { "id": 2, "title": "2-json-server", "author": "2-typicode" }

   Tests:
       tests["Verify status code"] = responseCode.code === 200;
       tests["Verify response body"] = responseBody.has("json-server");

   Result:
       PASS Verify status code
       PASS Verify response body
    ```

3. Update the record.

   ```json
   PUT http://localhost:3000/posts/2
   Request body: { "id": 2, "title": "2-json-server-updated", "author": "2-typicode-updated" }

   Response status code: "200 OK"
   Response body: { "id": 2, "title": "2-json-server-updated", "author": "2-typicode-updated" }
    ```

4. Verify updated record data.

   ```json
   GET http://localhost:3000/posts/2

   Response status code: "200 OK"
   Response body: { "id": 2, "title": "2-json-server-updated", "author": "2-typicode-updated" }

   Tests:
       tests["Verify status code"] = responseCode.code === 200;
       tests["Verify response body"] = responseBody.has("2-json-server-updated");

   Result:
       PASS Verify status code
       PASS Verify response body
    ```

5. Delete the record.

   ```json
   DELETE http://localhost:3000/posts/2

   Response status code: "200 OK"
   Response body: {}
    ```

6. Verify record data.

   ```json
   GET http://localhost:3000/posts/2

   Response status code: "404 Not Found"
   Response body: {}

   Tests:
        tests["Verify status code"] = responseCode.code === 404;
        tests["Verify response body"] = responseBody.has("{}");

   Result:
       PASS Verify status code
       PASS Verify response body
    ```

## Collections

Collections is a group of individual requests.

## Available properties

```javascript
Pre-req
-------
postman.setEnvironmentVariable("varName", "value");
console.log(postman.getEnvironmentVariable("varName"));

postman.clearEnvironmentVariable("varName");
// postman.clearEnvironmentVariables();

postman.setGlobalVariable("varName", "value");
console.log(postman.getGlobalVariable("varName"));

postman.clearGlobalVariable("varName");
// postman.clearGlobalVariables();

Tests
-----
console.log("request.data", request.data);
console.log("request.url", request.url);
console.log("request.method", request.method);

jsonResponse = JSON.parse(responseBody);
console.log("jsonResponse.title", jsonResponse.title);

console.log("responseTime", responseTime);
console.log("responseCode.code", responseCode.code);
console.log("responseCode.name", responseCode.name);
console.log("responseCode.detail", responseCode.detail);
```

## Chainning requests

tbd
