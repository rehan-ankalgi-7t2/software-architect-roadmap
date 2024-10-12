### HTTP
- `HTTP` is the protocol used to transfer data between a client (such as a web browser) and a server (such as a website). 
- When you visit a website, your web browser sends an HTTP request to the server, asking for the webpage or other resource you’ve requested. 
- The server then sends an HTTP response back to the client, containing the requested data.

### HTTPS
- `HTTPS` is a more secure version of HTTP, which encrypts the data being transmitted between the client and server using SSL/TLS (Secure Sockets Layer/Transport Layer Security) encryption.
- This provides an additional layer of security, helping to protect sensitive information such as login credentials, payment information, and other personal data.

When you visit a website that uses HTTPS, your web browser will display a padlock icon in the address bar, indicating that the connection is secure. You may also see the letters “https” at the beginning of the website address, rather than “http”.

## Most Common Headers

```jsx
accept: "application/json"
user-agent: ""
authorization: ""
cookie: ""
content-type: ""
cache-control: ""
```


## HTTP Methods

> a set of request methods to indicate the desired action to be performed for a given resource. Each HTTP request includes a method, which is a verb indicating the type of operation to be performed.
> 
1. **`GET`**: Retrieve data from the specified resource. The GET method should only retrieve data and should not have any other effect.
2. **`POST`**: Submit data to be processed to a specified resource. The data is included in the body of the request. It is often used when uploading a file or submitting a form.
3. **`PUT`**: Update a resource or create a new resource if it doesn't exist at the specified URL. The entire representation of the resource is replaced with the new one.
4. **`PATCH`**: Apply partial modifications to a resource. It is used to apply changes to a resource with the data provided in the body of the request.
5. **`DELETE`**: Request that a resource be removed or deleted. It should perform the deletion of the specified resource.
6. **`HEAD`**: Retrieve the headers of a resource, similar to the GET method, but without the response body. It is often used to check the existence and status of a resource.
7. **`OPTIONS`**: Retrieve information about the communication options available for a resource. It is used to describe the communication options for the target resource.
8. **`TRACE`**: Echoes the received request, so that a client can see what (if any) changes or additions have been made by intermediate servers.
9. **`CONNECT`**: Establishes a tunnel to the server identified by a given URL. It is often used to set up a secure SSL/TLS communication through an unsecured HTTP proxy.

<aside>
💡 These HTTP methods are fundamental building blocks of RESTful APIs and web services. When interacting with a web server or API, the client (such as a web browser or application) uses these methods to perform various actions on resources hosted on the server. Each method has a specific purpose, and their usage depends on the desired operation.

</aside>

---

## HTTP Status Codes

> `status codes` are three-digit numbers returned by a server in response to a client's request made to the server. They provide information about the status of the request. The status code is contained within the response header, and it is designed to be machine-readable.
> 

**`1xx Informational:`**

- **100 Continue:** The server has received the request headers and the client should proceed to send the request body.

**`2xx Success:`**

- **200 OK:** The request was successful, and the server has returned the requested data.
- **201 Created:** The request was successful, and a new resource was created as a result.
- **204 No Content:** The server successfully processed the request, but there is no additional information to send in the response.

**`3xx Redirection:`**

- **301 Moved Permanently:** The requested resource has been permanently moved to a new location.
- **302 Found (or Moved Temporarily):** The requested resource has been temporarily moved to another location.
- **304 Not Modified:** The resource has not been modified since the last request, and there is no need to retransmit the requested data.

**`4xx Client Error:`**

- **400 Bad Request:** The server cannot or will not process the request due to a client error (e.g., malformed request syntax, invalid request message framing, or deceptive request routing).
- **401 Unauthorized:** The request requires user authentication. The client must provide valid credentials to access the requested resource.
- **403 Forbidden:** The server understood the request, but it refuses to authorize it.
- **404 Not Found:** The requested resource could not be found on the server.

**`5xx Server Error:`**

- **500 Internal Server Error:** A generic error message returned when an unexpected condition was encountered on the server.
- **501 Not Implemented:** The server does not support the functionality required to fulfill the request.
- **503 Service Unavailable:** The server is not ready to handle the request. Common causes are a server that is down for maintenance or is overloaded.