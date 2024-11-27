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
