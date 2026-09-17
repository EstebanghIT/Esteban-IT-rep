# API & Postman Troubleshooting Lab

## Overview

A basic API support lab created to practice testing REST API endpoints with Postman and troubleshooting common request and response issues.

The lab focuses on skills that are useful in Technical Support and Application Support environments.

## What I Practiced

- Sending GET, POST, PUT and DELETE requests
- Testing REST API endpoints
- Reading JSON responses
- Checking HTTP status codes
- Working with request headers and parameters
- Sending JSON data in request bodies
- Testing incorrect endpoints
- Identifying basic API errors

## GET Request

I used Postman to send a GET request and retrieve data from a REST API.

I checked:

- HTTP status code
- Response body
- Response time
- Returned JSON data

A successful request returned `200 OK`.

## POST Request

I tested creating a resource by sending JSON data in the request body.

```json
{
  "name": "Test User",
  "role": "Support"
}
```

I then reviewed the response to confirm that the request was processed correctly.

## Error Troubleshooting

I intentionally tested incorrect requests to understand how API errors appear in Postman.

Some of the HTTP status codes reviewed were:

- 200 OK
- 201 Created
- 400 Bad Request
- 404 Not Found
- 500 Internal Server Error

When troubleshooting a failed request, I checked the endpoint URL, HTTP method, request headers, parameters, JSON body, status code, and response message.

## Support Scenario

A user reports that information from an application is not loading.

As an initial troubleshooting step, I can test the related API endpoint in Postman. If the API returns the expected data, the issue may need investigation at another layer of the application. If the API returns an error, the status code and response body provide useful information for troubleshooting or escalation.

## Tools Used

- Postman
- REST APIs
- HTTP
- JSON

## Skills Practiced

- API troubleshooting
- HTTP requests
- HTTP status codes
- JSON
- Request/response analysis
- Technical troubleshooting

## What I Learned

This lab helped me understand how Postman can be used to test API behavior and investigate application issues. I also practiced using HTTP responses and status codes to collect useful information before escalating a technical issue.
