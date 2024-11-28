### Steps to Create and Configure a Web Server with Nginx

1. **Create a Web Application and a Catalog Server**:
   - Set up a server instance using the `t2.micro` instance type on your cloud platform (like AWS, Azure, etc.).
   - Ensure that the server is properly initialized and has a public IP address assigned.

2. **Connect to the Server**:
   - Use an SSH client like PuTTY to connect to your server.
   - Enter the public IP address in PuTTY and log in using your credentials.

3. **Gain Root Access**:
   - Once connected, you will need root access to install software. You can obtain this by using the following command:
     ```bash
     sudo su -
     ```

4. **Install Nginx**:
   - As part of the web application setup, you will be installing Nginx, a popular web server.
   - Use the following command to install Nginx:
     ```bash
     dnf install nginx -y
     ```

5. **Enable and Start the Nginx Service**:
   - After installation, you need to enable the Nginx service to start on boot:
     ```bash
     systemctl enable nginx
     ```
   - Now, start the Nginx service to make your web server operational:
     ```bash
     systemctl start nginx
     ```

6. **Access the Nginx Service via Browser**:
   - To verify that Nginx is running correctly, open a web browser and type the following URL, replacing `public-ip` with your server's actual public IP address:
     ```
     http://public-ip:80
     ```
   - You should see the default Nginx welcome page, indicating that the web server is functioning.

7. **Remove Default Content**:
   - Once you confirm that Nginx is running, you may want to clear out the default content that comes with the installation. To do this, execute the following command:
     ```bash
     rm -rf /usr/share/nginx/html/*
     ```
   - This will remove any default files in the Nginx web directory, allowing you to add your own content.

By following these steps, you will have successfully set up a web server using Nginx. Make sure to customize it further according to your application needs!
 ````````
   
To download the project application code, please follow these steps to ensure it is saved in the temporary directory:

1. Open your terminal or command prompt.
2. Use the following command to download the application code as a zip file:

   ```bash
   curl -o /tmp/web.zip https://roboshop-builds.s3.amazonaws.com/web.zip
   ```

   In this command, replace `https://roboshop-builds.s3.amazonaws.com/web.zip` with the actual URL where the project application code is hosted. This will download the zip file directly into the `/tmp` directory on your system. After downloading, you can navigate to that directory to
access the project files.

1. **Navigate to the Nginx HTML Directory**  
   Open your terminal and change your directory to where Nginx serves its HTML files. You can do this by executing the following command:  
   ```bash
   cd /usr/share/nginx/html
   ```

2. **Extract the Application Files**  
   Once you are in the correct directory, you need to extract the contents of the application package. If you have a ZIP file containing the application in the `/tmp` directory, you can extract it using the `unzip` command. Run the following command to unzip the file:  
   ```bash
   unzip /tmp/web.zip
   ```  
   This will unpack all the files from `web.zip` into the current directory. Make sure to check for any additional files or directories created after extraction, as they may contain important components for your application.

To set up an Nginx reverse proxy configuration for your application, follow these detailed steps:

1. **Create or Edit the Nginx Configuration File**: Open your terminal and create or edit the configuration file located at `/etc/nginx/default.d/roboshop.conf`. You can do this using the `vim` text editor:

   ```bash
   vim /etc/nginx/default.d/roboshop.conf
   ```

proxy_http_version 1.1;
location /images/ {
  expires 5s;
  root   /usr/share/nginx/html;
  try_files $uri /images/placeholder.jpg;
}
location /api/catalogue/ { proxy_pass http://localhost:8080/; }
location /api/user/ { proxy_pass http://localhost:8080/; }
location /api/cart/ { proxy_pass http://localhost:8080/; }
location /api/shipping/ { proxy_pass http://localhost:8080/; }
location /api/payment/ { proxy_pass http://localhost:8080/; }

location /health {
  stub_status on;
  access_log off;
}
2. **Configure Proxy Settings**: In the configuration file, add the following content to define how Nginx will handle incoming traffic. This includes settings for image expiration, API forwarding, and health status reporting.

   ```nginx
   # Set the HTTP version for proxying
   proxy_http_version 1.1;

   # Configuration for image requests
   location /images/ {
       expires 5s;  # Set the expiration time for cached images to 5 seconds
       root /usr/share/nginx/html;  # Define the root directory for images
       try_files $uri /images/placeholder.jpg;  # Serve a placeholder image if the requested image doesn't exist
   }

   # API endpoint for catalogue services
   location /api/catalogue/ {
       proxy_pass http://localhost:8080/;  # Forward requests to the local service running on port 8080
   }

   # API endpoint for user services
   location /api/user/ {
       proxy_pass http://localhost:8080/;  # Proxy to the local service
   }

   # API endpoint for cart services
   location /api/cart/ {
       proxy_pass http://localhost:8080/;  # Proxy to the local service
   }

   # API endpoint for shipping services
   location /api/shipping/ {
       proxy_pass http://localhost:8080/;  # Proxy to the local service
   }

   # API endpoint for payment services
   location /api/payment/ {
       proxy_pass http://localhost:8080/;  # Proxy to the local service
   }

   # Health check endpoint
   location /health {
       stub_status on;  # Enable stub status to monitor health
       access_log off;  # Disable access logging for this location
   }
   ```

3. **Testing and Reloading Configuration**: After saving your changes to the configuration file, it's a good idea to test the Nginx configuration for any syntax errors. You can do this by running:

   ```bash
   sudo nginx -t
   ```

   If the test is successful, reload Nginx to apply the new configuration:
To restart the Nginx web server, you need to execute the following command in the terminal. This will stop the Nginx service and then start it again, ensuring that any changes made to the configuration files are applied. Use the command below:

```bash
sudo systemctl restart nginx
```

Make sure you have the appropriate permissions to run this command, as it often requires superuser access. If there are any issues during the restart, you can check the status of the Nginx service with the command:

```bash
sudo systemctl status nginx
```

This command will provide information about whether Nginx is running correctly or if there are any errors that need to be addressed.

When we want to access a website, the first step involves obtaining its domain name. For example, if we want to visit facebook.com, our device performs a series of checks to resolve the domain name into an IP address.

Initially, the device checks its own local cache to see if it has recently accessed facebook.com and has the corresponding IP address stored. If the address is not found in the local cache, the operating system then queries the Internet Service Provider (ISP) resolver, asking for the IP address associated with facebook.com.

The ISP resolver plays a crucial role in this process. It first examines its own cache to determine if the IP address for facebook.com is available there. If the ISP resolver does not have the address cached, it proceeds to contact the root name servers to obtain the necessary information.

Root servers are foundational components of the Domain Name System (DNS) and are responsible for directing queries to the correct Top-Level Domain (TLD) servers, such as those for .com, .org, etc. There are only 13 root servers worldwide, operated by various organizations that have voluntarily established them. To manage and distribute the load efficiently, these root servers are supported by numerous additional servers that assist with load balancing and redundancy.

Once the request reaches the appropriate TLD server, the ISP resolver can retrieve the IP address for facebook.com and return it to the user's device. This multi-tiered system ensures that domain name resolutions are efficient and reliable, allowing users to access websites promptly.

A TLD, or top-level domain, refers to the last segment of a domain name, which follows the final dot in the address. For instance, in the domain name "example.com," the TLD is ".com." TLDs are integral to the Domain Name System (DNS) and are categorized into several types, including:

1. **Generic TLDs (gTLDs)**: These are the most common and include extensions such as .com, .org, .net, and new gTLDs like .tech, .shop, and .blog.
  
2. **Country Code TLDs (ccTLDs)**: These are specific to a country or territory, such as .uk for the United Kingdom, .ca for Canada, and .jp for Japan.

3. **Sponsored TLDs (sTLDs)**: These are specialized domains that are restricted to a particular community and are sponsored by an organization. Examples include .edu for educational institutions and .gov for governmental entities.

Overall, the choice of a TLD can influence perceptions of credibility and trustworthiness, making it an essential aspect of online branding and identity.

The .com top-level domain (TLD) provides crucial information regarding name servers, which are essential components of the Domain Name System (DNS). These name servers play a pivotal role in translating human-readable domain names into IP addresses, enabling browsers to locate and access the resources associated with a specific website. When a domain is registered with a .com TLD, the associated name servers are configured to direct traffic to the correct server hosting the website, ensuring seamless connectivity for users.

**Domain Registrars Overview**

When it comes to registering a domain name for your website, there are several reputable registrars to consider. Here are three popular options:

1. **GoDaddy**: Known as one of the largest domain registrars in the world, GoDaddy offers a wide range of services including domain registration, web hosting, and website builders. They provide a user-friendly interface and often run promotions for new customers, making it easy to find and secure the perfect domain.

2. **Hostinger**: While primarily recognized for its affordable web hosting solutions, Hostinger also offers domain registration services. They provide competitive pricing and a variety of extensions, along with bundled services that can help streamline the process of launching a new website.

3. **Amazon Web Services (AWS)**: AWS, while commonly known for its cloud computing services, also provides domain registration through Route 53. This service is particularly appealing for businesses looking for scalability and reliability, as it integrates seamlessly with other AWS services, making it ideal for tech-savvy users and developers.

Each of these registrars has unique features tailored to different needs, whether you’re a beginner or an experienced web developer.


Hostinger's responsibility includes providing updates to Meenakshi regarding the domain purchased, which is daw80.online. The nameservers associated with this domain are as follows: ns1.dns-parking.com and ns2.dns-parking.com. Please ensure that Meenakshi is informed of these details for proper domain management and configuration.
i
--------------------------------
To effectively manage our domain using the ISP resolver approach, we are focusing specifically on the ".online" top-level domain (TLD). This process initiates with the ISP resolver, which will be queried to extract detailed information regarding the name servers that are linked to our domain.

Once we obtain these name server details, the ISP resolver will establish a secure connection with our web hosting provider, Hostinger. This connection is vital as it lays the groundwork for the necessary configurations that will support our domain's functionality.

As we operate on Amazon Web Services (AWS) for our cloud infrastructure, we aim to automate the creation of specific DNS records. This automation is critical for efficient domain management, ensuring that updates and changes can be made seamlessly without manual intervention.

A crucial aspect of this process involves transforming the existing name servers to align with our new configurations. After successfully creating a hosted zone in AWS, we acquired a set of name servers that will be tasked with handling all DNS queries related to our domain.

It is now imperative that Hostinger takes action to update the name servers corresponding to our ".online" TLD. This update is essential for proper DNS resolution, ensuring that all incoming traffic is directed to the correct web resources associated with our domain.

Furthermore, we need to establish an A record for our specific domain. When users enter "daws80.online" into their browser, the DNS should accurately resolve this query to the ".online" TLD. The system will then forward the request to the AWS-configured name servers, which are responsible for checking the corresponding IP address. This communication will enable us to direct users to our application smoothly, ensuring they can access the services we provide without any disruption.



When we search for the domain "joindeveops.online," the process of resolving that request involves several steps. Initially, the browser checks its own cache to see if it has previously stored the IP address associated with that domain. If the information is not found in the browser cache, the request is forwarded to the operating system (OS). The OS then checks its own cache to see if it has the necessary information saved from a prior lookup.

If the OS cache also lacks the needed information, the request is then sent to the Internet Service Provider (ISP) resolver. The ISP resolver first checks its own cache for the IP address associated with "joindeveops.online." If the IP address is still not found, the ISP resolver must escalate the request by querying the root DNS servers.

The root servers play a crucial role in the Domain Name System (DNS) hierarchy. Upon receiving the request, they scan their records to determine the top-level domain (TLD) associated with the query, which in this case is ".online." After identifying the TLD, the root server provides the ISP resolver with the nameservers responsible for handling requests for ".online" domains.

Next, the ISP resolver contacts the nameservers for the ".online" TLD, particularly the nameservers hosted by AWS (Amazon Web Services). These nameservers have the authoritative records for the domain. Once the nameservers receive the query from the ISP resolver, they look up the specific DNS records related to "joindeveops.online."

The nameservers then return the corresponding IP address linked to the domain. With the IP address in hand, the browser can now send a request directly to that IP address, allowing the user to access the desired website. This multi-step resolution process illustrates the complex workings behind simple web browsing.



browser - itscache -os -its cache - isp -its cache  -  root servers - TLD - NS -A records


The process of resolving a domain name into an IP address is a fundamental function of the Domain Name System (DNS). Understanding how this process occurs involves examining each step in detail, particularly the role of caching and the various components involved:

### 1. User’s Device and Browser (Cache)
When you enter a domain name (for example, example.com) into your web browser, the first action is to check the browser's cache for a previously resolved IP address. 

- **Browser Cache Verification**: 
  - The browser searches its internal cache to determine if the IP address associated with the domain has been stored recently.
  - If a valid entry is found—meaning the cached information isn't expired—the browser utilizes that IP address to initiate a connection to the website without any further resolution steps.
  - If no valid entry exists, the browser then queries the operating system (OS) for the information.

### 2. Operating System (OS Cache)
The operating system also maintains a DNS resolver, which holds a cache of recently resolved domain names and their corresponding IP addresses.

- **OS Cache Check**:
  - When the browser doesn't find the IP address, the OS checks its DNS resolver cache.
  - If the domain is found in the OS cache, the process concludes, and the cached IP address is used.
  - If not present, the OS resolver sends a request to the Internet Service Provider's (ISP) DNS server for resolution.

### 3. ISP DNS Server (Cache)
The ISP acts as an intermediary in the DNS resolution process and has its own cache of previously resolved domains to optimize lookup speed and efficiency.

- **ISP Cache Usage**:
  - Upon receiving the query from the OS, the ISP's DNS server checks its cache for the required IP address.
  - If the ISP’s server has the address, it immediately returns the resolved IP to the OS, effectively completing the resolution process.
  - If the IP is not in the ISP's cache, the server forwards the request to one of the root DNS servers.

### 4. Root Servers
Root DNS servers play a critical role in the hierarchy of DNS. 

- **Directing the Query**:
  - These servers do not directly resolve domain names to IP addresses but instead provide the addresses of the appropriate Top-Level Domain (TLD) servers.
  - For example, if the query is for example.com, the root server will guide the request to the TLD server that handles .com domains.

### 5. TLD Servers
Once the query reaches the TLD server, it further processes the request.

- **TLD Server Operations**:
  - The TLD server holds information about all the domains under its purview (like .com, .org, etc.) and responds to the request by providing the address of the authoritative name server responsible for the specific domain in question (e.g., example.com).

### 6. Authoritative Name Server (NS)
The authoritative name server is the ultimate source of truth for the specific domain.

- **Final Resolution**:
  - This server contains the actual DNS records, including the A record (for IPv4 addresses) or the AAAA record (for IPv6).
  - When the authoritative name server receives the request, it replies with the IP address associated with the domain name.

### 7. Cache and Response
The resolved IP address then travels back through the DNS hierarchy.

- **Return Path and Caching**:
  - The IP address is returned first to the ISP's DNS server, then to the OS, and finally back to the web browser.
  - Each layer involved in the resolution process caches the IP for future queries, which significantly speeds up subsequent access to the same domain by avoiding redundant lookups.

### Key Records in DNS
Understanding the various DNS record types and their purpose is critical for comprehending DNS operations:

- **Root Servers**: Provide addresses for TLD servers.
- **TLD Servers**: Relay information regarding authoritative NS addresses.
- **NS (Name Server) Records**: Point to the authoritative name server for the domain.
- **A Record**: Maps a domain name to its corresponding IPv4 address.
- **Caching Layers**: The ISP and operating system caches intermediate results to optimize DNS resolution time during subsequent requests.

In summary, this multi-layered DNS resolution process ensures that users can access websites quickly and efficiently, with significant reliance on caching at various steps to reduce the load on DNS servers and improve response times.


MONGODB INSTALLATION:
------------------------------
To launch a new instance, select the T3.Medium instance type, and then connect to it using PuTTY. 

Once you have successfully accessed your instance, proceed to set up the MongoDB repository by creating or editing the repository file. You can do this by using the `vim` text editor. Open the terminal and enter the following command:

```bash
vim /etc/yum.repos.d/mongo.repo
```

In the `mongo.repo` file, add the following configuration for MongoDB version 4.2:

```
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=0
enabled=1
```

Make sure to replace `https://repo.mongodb.org/yum/redhat/` with the actual URL for the MongoDB repository. 

After making these changes, save and exit the file. This will set up the necessary repository to allow you to install and manage MongoDB on your instance effectively.


### Step-by-Step Guide to Install and Configure MongoDB

#### Step 1: Install MongoDB
To install MongoDB on your server, use the following command:
```bash
sudo dnf install mongodb-org -y
```
This command utilizes the package manager `dnf` to install the MongoDB package, where the `-y` flag automatically confirms the installation prompts.

#### Step 2: Enable and Start the MongoDB Service
After installing MongoDB, you need to enable and start the MongoDB service to ensure it starts on boot and runs immediately. Execute the following commands:
```bash
sudo systemctl enable mongod
sudo systemctl start mongod
```
- The `enable` command configures the MongoDB service to start automatically during system boot.
- The `start` command starts the MongoDB service right away.

#### Step 3: Configure MongoDB for Remote Access
By default, MongoDB is configured to accept connections only from the localhost (the local machine). This is a security measure to restrict access to your database. If you need to allow a remote server to access your MongoDB instance, you'll have to modify the configuration file.

1. Open the MongoDB configuration file in a text editor. You can use `vim` or any other text editor of your choice:
   ```bash
   sudo vim /etc/mongod.conf
   ```

2. Look for the `bindIp` configuration setting that typically looks like this:
   ```yaml
   bindIp: 127.0.0.1
   ```
   Change this setting to include the IP address of the remote server (0.0.0.0) that you want to allow access. You can specify multiple IP addresses separated by commas. For example:
   ```yaml
   bindIp: 127.0.0.1,0.0.0.0
   ```

3. Save the changes and exit the editor.

#### Step 4: Restart the MongoDB Service
For the changes to take effect, you need to restart the MongoDB service. Use the following command:
```bash
sudo systemctl restart mongod
```
This command restarts the MongoDB service to apply the new configuration settings.

By following these steps, you can successfully install MongoDB and configure it to accept connections from a remote server. Always ensure that you follow best practices for security when allowing remote access to your database.


catalogue installation:
------------------------------
