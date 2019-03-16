# NGINX Fundamentals

*Based on the Udemy´s course - [Nginx Fundamentals - High Performance Servers from Scratch]*
(https://www.udemy.com/nginx-fundamentals/)

#

## 1. About NGINX

- High Performance :truck:;

- High Concurrency :globe_with_meridians:;

- Low resource usage :battery:.

#

- **Basic HTML Virtual Host**

```
http {
    server {
        listen 80;
        server_name yourdomain.com;
        index index.html;

        location / {
            default_type "text/html";
            try_files $uri.html $uri /index.html;
        }

        # Adds Video Streaming
        location /video/ {
            mp4;
        }
    }
}
```

#

- **NGINX vs Apache**

  - **Apache:** By default, Apache is configured in what's called prefork mode, meaning that had spawned a set number of processors, each of which can serve a single request at a time regardless of whether that request is for a PHP script or an image.

  <p align="center"><img src="images/apache1.png" width="400px"></p>

  - **NGINX:** NGINX deals with the requests asynchronously, meaning that a single NGINX process can serve multiple requests concurrently, with that number basically just depending on the system resources available to the NGINX process.

      NGINX, unlike Apache, can't embed server side programming languages into its own processes, meaning that all requests for Dynamic Content has to be dealt with by a completely separate process like PHP-FPM *(FastCGI Process Manager)* and then reverse proxy back to the client via NGINX.

  <p align="center"><img src="images/nginx1.png" width="700px"></p>

#

  - **Apache:** Apache accepts a preconfigured number of requests, rejecting the rest.

  <p align="center"><img src="images/apache2.png" width="350px"></p>

  - **NGINX:** NGINX will serve static resources without the need to involve any server side languages. NGINX also can handle concurrent requests and potentially receive thousands of requests in a single processing thread, and respond to them as fast as it can without turning down any of those requests. These features make NGINX provides **faster static resources** and **higher concurrency** than Apache.  

  <p align="center"><img src="images/nginx2.png" width="500px"></p>

#

**How to install NGINX from Source Code with additional modules**

_The additional modules cannot be installed by package manager_

- Download the source code:

  `$ wget https://nginx.org/download/nginx-1.15.9.tar.gz`

- Extract the source code:

  `$ tar -xzvf nginx-1.15.9.tar.gz`

- Install the system dependencies:

  `$ apt install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev`

  or

  `$ yum install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev`

- Install NGINX with custom configuration:

  `$ ./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module`

  `$ make`

  `$ make install`

  `$ nginx -V` _Check the Nginx's version_

  `$ nginx` _Start the Nginx_

  `$ nginx -s <signal>` _Send a signal to Nginx, like stop, start, reload, etc._

#

**Adding an NGINX Service**

- Create the NGINX systemd service file:

  `$ touch /lib/systemd/system/nginx.service`

- Paste the content in the NGINX systemd service file _(https://www.nginx.com/resources/wiki/start/topics/examples/systemd/)_:

  ```
    [Unit]
    Description=The NGINX HTTP and reverse proxy server
    After=syslog.target network.target remote-fs.target nss-lookup.target

    [Service]
    Type=forking
    PIDFile=/var/run/nginx.pid
    ExecStartPre=/usr/bin/nginx -t
    ExecStart=/usr/bin/nginx
    ExecReload=/usr/bin/nginx -s reload
    ExecStop=/bin/kill -s QUIT $MAINPID
    PrivateTmp=true

    [Install]
    WantedBy=multi-user.target
  ```

- Start the NGINX service:

  `$ systemctl start nginx`

- Set NGINX to start in boot:

  `$ systemctl enable nginx`

#

**Understanding Configuration Terms**

- **Directives:**

  `server_name mydomain.com;`

- **Contexts:** Are the sections within the configuration where directives can be set for that given context.

  [[Article] Understanding the Nginx Configuration File Structure and Configuration Contexts](https://www.digitalocean.com/community/tutorials/understanding-the-nginx-configuration-file-structure-and-configuration-contexts)

  - **Main context:** Is where we configure global directives that apply to the master process.

  <p align="center"><img src="images/maincontext.png" width="500px"></p>

  - **HTTP Context:** It contains anything for HTTP related.

  ```
  http {
    index index.html;

    server {
      server_name www.domain1.com;
      access_log logs/domain1.access.log main;

      root /var/www/domain1.com/htdocs;
    }

    server {
      server_name www.domain2.com;
      access_log  logs/domain2.access.log main;

      root /var/www/domain2.com/htdocs;

      location /some_path {
        add_header header_name header_value;
      }
    }
  }
  ```

  - **Server context:** is where we define a virtual host similar to an Apache V host.

  ```
    server {
      server_name www.domain2.com;
      access_log  logs/domain2.access.log main;

      root /var/www/domain2.com/htdocs;

      location /some_path {
        add_header header_name header_value;
      }
    }
  ```

  - **Location context:** Is used for matching URI locations on incoming requests to the parent server context.

  ```
    location /some_path {
      add_header header_name header_value;
    }
  ```  

#

**Creating a virtual host**

- /etc/nginx/nginx.conf

  ```
    events {}

      http {

        include mime.types;

          server {

            listen 80;
            server_name 167.99.93.26;

            root /sites/demo;
          }
      }
  ```

- Test Nginx's syntax:

  `$ nginx -t`

- Reload Nginx:

  `$ systemctl reload nginx`

- Test Nginx delivery with curl:

  `$ curl -I http://167.99.93.26/index.html`

#

**Location Blocks**

- Location Block basic syntax:

  ```
    server {
      location URI {
        ...handle response
      }
    }
  ```

- My Location Block conf example:

  ```
    events {}

    http {

      include mime.types;

      server {

        listen 80;
        server_name 172.31.95.110;

        root /sites/demo;

        location /healthcheck {
           return 200 'WORKING';
        }
      }
    }
  ```

- Course Location Block example:

  ```
    events {}

    http {

      include mime.types;

      server {

        listen 80;
        server_name 167.99.93.26;

        root /sites/demo;

        # Preferential Prefix match
        location ^~ /Greet2 {
          return 200 'Hello from NGINX "/greet" location.';
        }

        # # Exact match
        # location = /greet {
        #   return 200 'Hello from NGINX "/greet" location - EXACT MATCH.';
        # }

        # # REGEX match - case sensitive
        # location ~ /greet[0-9] {
        #   return 200 'Hello from NGINX "/greet" location - REGEX MATCH.';
        # }

        # REGEX match - case insensitive
        location ~* /greet[0-9] {
          return 200 'Hello from NGINX "/greet" location - REGEX MATCH INSENSITIVE.';
        }
      }
    }
  ```  

#

**Variables**

- **Configuration Variables:**

  - set $var 'something';

- **NGINX Module Variables:**

  - $http, $uri, $args

- **NGINX Alphabetical index of variables:**

- http://nginx.org/en/docs/varindex.html

- **Article:** [If is Evil](https://www.nginx.com/resources/wiki/start/topics/depth/ifisevil/)

#

**Rewrites and Redirects**

- **Rewrite directive:**

  `rewrite pattern URI`

- **Return directive:**

  `return status URI`

- The standard return statement takes a status code and a data or string sentence:

  _return_ **200** "Hello World",  

- If the response code being a **300** variant, which is for a redirect statement, the return directives behaviour changes and then excepts an URI as the second parameter A URI to which the client should be redirected:

  _return_ **307** /some/path;

- **Redirect example:**

    ```
    events {}

    http {

      include mime.types;

      server {

        listen 80;
        server_name 172.31.95.110;

        root /sites/demo;

        rewrite ^/user/\w+ /greet;

        location /greet {
            return 200 "Hello User";
        }
       }
    }
    ```

- **Difference between rewrites and redirects:**

  - **Redirects:** A redirect simply tells the client that performing the request where to go instead:

  <p align="center"><img src="images/redirect1.png" width="500px"></p>

  <p align="center"><img src="images/redirect2.png" width="500px"></p>

  - **Rewrites:** A rewrite mutates the URI internally:

  <p align="center"><img src="images/rewrite1.png" width="500px"></p>

  <p align="center"><img src="images/rewrite2.png" width="500px"></p>

  <p align="center"><img src="images/rewrite3.png" width="500px"></p>

- **Redirect Example:**

    ```
      events {}

      http {

        include mime.types;

        server {

          listen 80;
          server_name 172.31.95.110;

          root /sites/demo;

          location /healthcheck {
             return 200 'WORKING';
          }

          location /logo {
             return 307 /thumb.png;
           }
         }
      }
    ```

- **Try-Files and Named Locations**

  - Try-Files as with the return and rewrite directives, can be used in the _server context_. Applying to all incoming requests or inside a location context.

  ```
    server {
      try_files path1 path2 final; (Server context)
      location / {
        try_files path1 path2 final; (Location context)
      }
    }
  ```

  - What Try-files allows us to do is have Nginx check for a resource to respond worth in number of locations relative to the root directory with a final argument that result in a rewrite and re-evaluation as the rewrite directive.

  - **Try-files example:**

    ```
      events {}

      http {

        include mime.types;

        server {

          listen 80;
          server_name 172.31.95.110;

          root /sites/demo;

          try_files $uri /cat.png /greet /friendly_404;

          location /friendly_404 {
             return 404 'Sorry, that file could not be found.';
          }

          location /greet {
             return 200 "Hello User";
           }
         }
      }
    ```

  - **Named Locations**

    - Named Location simply means assigning a name to a location context and using a directive, such as try-files.  
