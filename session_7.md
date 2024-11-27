### Roboshop Configuration

**Security Considerations**
Companies often enforce security measures, which may include restrictions on using certain websites, prohibitions on file uploads, and monitoring of internet usage behavior. This helps ensure a safe computing environment by controlling the exposure to potentially harmful content and activities.

**Proxy Awareness**
Clients are usually aware of the existence of proxy servers; however, the servers themselves may not be aware of the identities or details of the clients connecting through them.

**Reverse Proxy**
A reverse proxy acts as an intermediary for requests from clients seeking resources from servers. Clients remain unaware of the server-side arrangements, meaning they interact solely with the reverse proxy. This setup is beneficial for several reasons:
- It can be used to secure application code by hiding the actual server details from clients.
- It provides functionalities such as load balancing, distributing client requests across multiple servers to ensure no single server is overwhelmed.

**API Usage Example**
When accessing an API endpoint such as `http://54.197.5.96/api/catalogue/categories`, clients can query the product catalogue to retrieve information about available product categories efficiently.

### HTTP Status Codes

**Successful Responses (2xx)**
Responses in the 2xx range indicate successful interactions between the client and server.

**Redirection Responses (3xx)**
Responses in the 3xx range indicate that requests have been redirected temporarily. This is often used for multimedia resources such as images and GIFs, which might be served from different locations.

**Client-Side Errors (4xx)**
- **400**: Bad Request - The server cannot process the request due to a client error.
- **403**: Forbidden - The server understands the request but refuses to authorize it.
- **404**: Not Found - The requested resource could not be found on the server.
- **402**: Payment Required - Reserved for future use.

**Server-Side Errors (5xx)**
Responses in the 5xx range indicate issues with the server itself, which are unrelated to the client's request. These are often seen as "purely project errors," suggesting that something went wrong in the application or server processing.

### MongoDB Overview

Understanding the differences between forward and reverse proxies is critical, particularly how they handle data and manage client requests.

**Caching Mechanisms**
Consider a practical example of caching: If an Airtel server has 1,000 users, and one user downloads the movie "Bahubali" from a server located in the US, that content is saved on a cache server. When a second user tries to access "Bahubali," they can retrieve it directly from the cache server, significantly enhancing speed and performance.

**Localhost Usage**
In network configurations, `127.0.0.1` may refer to the localhost, where services can be tested and run on the local machine without external exposure.

### Installation and Configuration Commands
To install and start the Nginx web server on a CentOS system, the following commands can be used:
```bash
dnf install nginx -y
systemctl start nginx
```

### Additional Resources
- **API Access Example**: Accessing the catalogue can be done using the endpoint `http://54.197.5.96/api/catalogue/categories`.
- **304 Not Modified**: A 304 status indicates that the resource requested has not been modified since the last accessed, allowing the client to use the cached version.

### Assignment Focus
1. Understand and document HTTP status codes.
2. Analyze the differences between forward proxies and reverse proxies.
3. Configure your project to utilize these concepts effectively.

**Development Practice Repository**: Refer to the `devops-practice` repository for insights and configurations. Utilize the CentOS environment with the designation `DevOps321` for relevant setups and practice.
