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
   
