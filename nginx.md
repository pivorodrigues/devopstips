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

## 2. Installation

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

## 3. Configuration

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

[Article [If is Evil]](https://www.nginx.com/resources/wiki/start/topics/depth/ifisevil/)

- **Configuration Variables:**

  - set $var 'something';

- **NGINX Module Variables:**

  - $http, $uri, $args

- **NGINX Alphabetical index of variables:**

- http://nginx.org/en/docs/varindex.html

  - **Variables conf example:**

    ```
      events {}

      http {

        include mime.types;

        server {

          listen 80;
          server_name 167.99.93.26;

          root /sites/demo;

          set $mon 'No';

          # Check if weekend
          if ( $date_local ~ 'Monday' ) {
            set $mon 'Yes';
          }



          location /is_monday {

            return 200 $mon;
          }
        }
      }
    ```  

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

    - Named Location simply means assigning a name to a location context and using a directive, such as try-files. Use that location by its name, ensuring no re-evaluation has to happen on that final argument, but, instead, just a definitive call to the name location.

    ```
      events {}

      http {

        include mime.types;

        server {

          listen 80;
          server_name 167.99.93.26;

          root /sites/demo;


          try_files $uri /cat.png /greet @friendly_404;

          location @friendly_404 {
            return 404 "Sorry, that file could not be found.";
          }


          location /greet {
            return 200 "Hello User";
          }

        }
      }
    ```

#

**Logging**

  [[Article] Configuring Logging](https://docs.nginx.com/nginx/admin-guide/monitoring/logging/)

  - Nginx provides us two log files for standard: **access.log** and **error.log**.

  - **Log files:** _(As our installation)_

    - **error.log:** `--error-log-path=/var/log/nginx/error.log`

    - **access.log:** `--http-log-path=/var/log/nginx/access.log`

  _OBS:_ Keep in mind that 404 is a perfectly valid response and by no means an error in itself.

  - **Logging conf example:**

  ```
    events {}

    http {

      include mime.types;

      server {

        listen 80;
        server_name 167.99.93.26;

        root /sites/demo;

        location /secure {

          # Add context specific log
          access_log /var/log/nginx/secure.access.log;

          # Disable logs for context
          #access_log off;

          return 200 "Welcome to secure area.";
        }

      }
    }
  ```

#

**Inheritance and Directive Types**

 - We have three directive types:

  1. Array Directive

  2. Standard Directive

  3. Action Directive

 - **Inheritance Directives Example:**  

 ```
   events {}

   ######################
   # (1) Array Directive
   ######################
   # Can be specified multiple times without overriding a previous setting
   # Gets inherited by all child contexts
   # Child context can override inheritance by re-declaring directive
   access_log /var/log/nginx/access.log;
   access_log /var/log/nginx/custom.log.gz custom_format;

   http {

     # Include statement - non directive
     include mime.types;

     server {
       listen 80;
       server_name site1.com;

       # Inherits access_log from parent context (1)
     }

     server {
       listen 80;
       server_name site2.com;

       #########################
       # (2) Standard Directive
       #########################
       # Can only be declared once. A second declaration overrides the first
       # Gets inherited by all child contexts
       # Child context can override inheritance by re-declaring directive
       root /sites/site2;

       # Completely overrides inheritance from (1)
       access_log off;

       location /images {

         # Uses root directive inherited from (2)
         try_files $uri /stock.png;
       }

       location /secret {
         #######################
         # (3) Action Directive
         #######################
         # Invokes an action such as a rewrite or redirect
         # Inheritance does not apply as the request is either stopped (redirect/response) or re-evaluated (rewrite)
         return 403 "You do not have permission to view this.";
       }
     }
   }
  ```

#

**PHP Processing**

[[Article] Understanding and Implementing FastCGI Proxying in Nginx](https://www.digitalocean.com/community/tutorials/understanding-and-implementing-fastcgi-proxying-in-nginx)

- Nginx isn't able to embed its server side language processors. So, instead the, we need to configure a standalone PHP service named php-fpm, to which Nginx will pass the request for processing and then upon receiving the response, typically a html, returning that to the client.  

<p align="center"><img src="images/nginx-php1.png" width="500px"></p>

...

<p align="center"><img src="images/nginx-php2.png" width="500px"></p>

...

<p align="center"><img src="images/nginx-php3.png" width="500px"></p>

...

**Configuring the PHP:**

  1. _Install the latest stable version of php-fpm:_

  `$ apt install php-fpm -y`

  2. _Check the php-fpm installation:_

  `$ systemctl list-units | grep php`

  and

  `$ systemctl status php7.2-fpm`

  - **PHP Conf Example:**

  ```
    user www-data;

    events {}

    http {

      include mime.types;

      server {

        listen 80;
        server_name 167.99.93.26;

        root /sites/demo;

        index index.php index.html;

        location / {
          try_files $uri $uri/ =404;
        }

        location ~\.php$ {
          # Pass php requests to the php-fpm service (fastcgi)
          include fastcgi.conf;
          fastcgi_pass unix:/run/php/php7.1-fpm.sock;
        }

      }
    }
  ```

#

**Worker Processes**

- The master process is the actual Nginx service or software instance which we started. The master process or Nginx itself. Then spawns work processes which listens for and response to client requests. The default number of worker processes for Nginx is one.

<p align="center"><img src="images/nginx_processes.png" width="500px"></p>

- We have two directives: **worker_processes_ and **worker_connections**.

- The **worker_processes** directive: we can change the number of Nginx worker processes setting in the conf file (/etc/nginx/nginx.conf):

  `worker_processes 2;`

<p align="center"><img src="images/nginx_processes_0.png" width="500px"></p>

- Increasing the number of workers Nginx spawns doesn't necessarily results in better performance. Nginx workers handle the process requests assynchronously. They will handle incoming requests as fast as their hardware are capable of. Creating a second worker process simply does not increase the harware's performance. One core of a cpu cannot share processes. A single Nginx worker process can only ever run on a sigle CPU call. We can 99% of the time configure Nginx to run the exact number of processes as the server CPU has.

<p align="center"><img src="images/nginx_cpu.png" width="500px"></p>

- If you are tempted to create a higher number of worker processes in the hope that your server will perform better, think of two worker processes on a single core as having two workers capable of only running at 50 percent.

<p align="center"><img src="images/nginx_cpu_0.png" width="250px"></p>

- When we set the _worker_processes_ directive to _auto_, Nginx will spawn one worker for each cpu core, as we can see below.

  ```
    user www-data;

    worker_processes auto;

    events {}

    http {

      include mime.types;

      server {

        listen 80;
        server_name 167.99.93.26;

        root /sites/demo;

        index index.php index.html;

        location / {
          try_files $uri $uri/ =404;
        }

        location ~\.php$ {
          # Pass php requests to the php-fpm service (fastcgi)
          include fastcgi.conf;
          fastcgi_pass unix:/run/php/php7.2-fpm.sock;
        }

      }
    }
  ```

<p align="center"><img src="images/nginx_processes_0.png" width="500px"></p>

- _OBS:_ To discover how cpu's do we have in our server, we have to those commands:

  `$ nproc`

  or

  `$ lscpu`

- The **worker_connections** directive: sets the number of connections each worker process can accept. It's not a number that we can simply increase. The server has a limit that how many files can be opened at once. We can check the file limit running the command `$ ulimit -n`. We can set this directive to that number in order to really max out the server.

  ```
    user www-data;

      worker_processes auto;

      events {
        worker_connections 1024;
      }

      http {

        include mime.types;

        server {

          listen 80;
          server_name 167.99.93.26;

          root /sites/demo;

          index index.php index.html;

          location / {
            try_files $uri $uri/ =404;
          }

          location ~\.php$ {
            # Pass php requests to the php-fpm service (fastcgi)
            include fastcgi.conf;
            fastcgi_pass unix:/run/php/php7.2-fpm.sock;
          }

        }
      }
  ```

- We now also have the maximum number of concurrent requests our server should be able to accept. As each of those work_processes can open the set number of connections or requests. These two directives _(processes and connections)_ being the most important to understand in order to really optimize the Nginx's process for performance.

<p align="center"><img src="images/nginx_max_conn.png" width="500px"></p>

- **The PID directive:** This directive allow us to reconfigure the process ID _(PID)_ location via the configuration file.

  ```
    user www-data;

      #pid /var/run/new_nginx.pid;

      worker_processes auto;

      events {
        worker_connections 1024;
      }

      http {

        include mime.types;

        server {

          listen 80;
          server_name 167.99.93.26;

          root /sites/demo;

          index index.php index.html;

          location / {
            try_files $uri $uri/ =404;
          }

          location ~\.php$ {
            # Pass php requests to the php-fpm service (fastcgi)
            include fastcgi.conf;
            fastcgi_pass unix:/run/php/php7.2-fpm.sock;
          }

        }
    }
  ```

#

**Buffers and Timeouts**

[[Article] Configuration file measurement units](http://nginx.org/en/docs/syntax.html)

- **Buffering:** Buffer is when a process or an Nginx worker reads data into memory or RAM before writing to its next destination.

<p align="center"><img src="images/nginx_buffer1.png" width="400px"></p>

- Nginx receives  a request which it reads from a TCP port (80), writes that request data to memory, which is buffering. Or, if the buffer is too small for the amount of data being read, writes some of it to disk.

<p align="center"><img src="images/nginx_buffer2.png" width="500px"></p>

- **Timeouts:** They simply suggest a cut off time for a given event. If a receiving request froma client stops after a certain number of seconds, this preventing a client from sending an endless stream of data and eventually breaking the server.

<p align="center"><img src="images/timeouts.png" width="400px"></p>

- **Buffering directives:**

  - **client_body_buffer_size:** This directive sets the amount of memory to allocate for buffering the POST data from a client. Post data most likelly coming from a form submission which in this case is set to 10k _(Kilobytes)_.

    ```
      # Buffer size for POST submissions
      client_body_buffer_size 10K; <---
      client_max_body_size 8m;
    ```

  - **client_max_body_size:** This directive sets the maximum acceptable size of POST requests. In this case, meaning don´t accept POST requests of more than 8 megabytes. If it is large than 8 megabytes, the server will respond with a **413** error, which means **Request Entity too Large**. This being a safety measure to ensure a user doesn´t mistakenly or maliciously send a very large POST request, which could cause the server to slow down, use a lot of disk space, etc.

    ```
      # Buffer size for POST submissions
      client_body_buffer_size 10K;
      client_max_body_size 8m; <---
    ```

  - **client_header_buffer_size:** As the name suggests, the amount of memory to allocate to reading request headers. 1 kilobyte is more than enough for 99% of requests. It is typically  being a small amount of data.

    ```
      # Buffer size for Headers
      client_header_buffer_size 1k;
    ```

  - **client_body_timeout and client_header_timeout:** In this case, the body timeout does not refer to the time it takes to transmit the entire request body, but rather the time between consecutive read operations. Those reads that happen to the buffer. In the example, the setting means 12 milliseconds.

    ```
      # Max time to receive client headers/body
      client_body_timeout 12;
      client_header_timeout 12;
    ```  

  - _OBS: Nginx allows us to sit times as follows in example below._

   <p align="center"><img src="images/nginx_time_directive.png" width="300px"></p>

  - **keepalive_timeout:** This directive sets the amount of time Nginx should keep a connection client open for in case more data is on the way. This is extremely useful when a client is requesting a number of files and keeping a connection open reduces the time it takes to open another new connection. Equally not wanting to leave connections open for too long as this can result in a pool of max connections being used up. For the most part, there´s no reason a connection would have to stay open beyond a few milliseconds before continuing. The most clients will close connections properly, meaning this timeout won't even apply.

    ```
      # Max time to keep a connection open for
      keepalive_timeout 15;
    ```  

  - **send_timeout:** If a client does not receive any of the response data in this amount of time, doesn't have to be all of the response data, but none of it at all. A boughts ending the response all together.

    ```
      # Max time for the client accept/receive a response
      send_timeout 10;
    ```

  - **sendfile:** Meaning when sending a client data from disk, like static files like images, don't use a buffer. Read that data from the disk and write it directly to the response.

  ```
    # Skip buffering for static files
    sendfile on;
  ```

  <p align="center"><img src="images/sendfile.png" width="500px"></p>

  - **tcp_nopush:** Enables Nginx to optimize the size of those data packets being sent to the client.

  ```
    # Optimise sendfile packets
    tcp_nopush on;
  ```

- **Buffers and Timeouts conf example:**

  ```
  user www-data;

  worker_processes auto;

  events {
  worker_connections 1024;
  }

  http {

    include mime.types;

    # Buffer size for POST submissions
    client_body_buffer_size 10K;
    client_max_body_size 8m;

    # Buffer size for Headers
    client_header_buffer_size 1k;

    # Max time to receive client headers/body
    client_body_timeout 12;
    client_header_timeout 12;

    # Max time to keep a connection open for
    keepalive_timeout 15;

    # Max time for the client accept/receive a response
    send_timeout 10;

    # Skip buffering for static files
    sendfile on;

    # Optimise sendfile packets
    tcp_nopush on;

    server {

      listen 80;
      server_name 167.99.93.26;

      root /sites/demo;

      index index.php index.html;

      location / {
        try_files $uri $uri/ =404;
      }

      location ~\.php$ {
        # Pass php requests to the php-fpm service (fastcgi)
        include fastcgi.conf;
        fastcgi_pass unix:/run/php/php7.1-fpm.sock;
      }

    }
  }
  ```
#

**Adding Dynamic Modules**

[[Article] ngx_http_image_filter_module](http://nginx.org/en/docs/http/ngx_http_image_filter_module.html)

  - To add dynamic modules, we have to rebuild Nginx from source. Dynamic Modules are modules that we can load selectively from the Nginx configuration, unlike static modules, which are always loaded.

  <p align="center"><img src="images/nginx_modules.png" width="400px"></p>

  - **Installing Nginx Dynamic Modules:**

    `$ cd /root/nginx-1.15.0` _(Goes to Nginx downloaded source code directory)_

    `$ nginx -V` _(Shows the Nginx install parameters)_

    `$ ./configure --help` or `./configure --help | grep -i dynamic` _(Lists all the Nginx's install flags to available modules and configurations)_

    `$ apt install libgd-dev` _(Installs the required library)_

    `$ ./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module --with-http_image_filter_module=dynamic --modules-path=/etc/nginx/modules` _(Rebuilds the Nginx with http image filter dynamic module)_

    `$ make` _(Prepares the Nginx package to finish the installation)_

    `$ make install` _(Finishes the installation)_

    `$ nginx -V` _(Checks the Nginx installation)_

    `$ systemctl reload nginx` _(Reloads the Nginx)_

    `$ systemctl status nginx` _(Checks the Nginx status)_

  - **To load installed dynamic modules:**

    - Add the the module directive in the main context of Nginx's conf file:

      `load_module modules/<module name>`

      or

      `load_module modules/ngx_http_image_filter_module.so` _(Example)_

#

## 4. Performance

**Headers and Expires**

  - Expires headers are essentially a response header informing the client or browser how long it can cache that response for.

  <p align="center"><img src="images/nginx_expires_1.png" width="400px"></p>

  - We can tell the browser to cache a copy of an object for a relatively long time. And doing so avoid any future requests for that object drastically improving the website load times and often overlook a reduction in requests to our server.

  <p align="center"><img src="images/nginx_expires_2.png" width="400px"></p>

  <p align="center"><img src="images/nginx_expires_3.png" width="400px"></p>

  - **Headers and Expires conf example:**

    ```
    user www-data;

    worker_processes auto;

    events {
      worker_connections 1024;
    }

    http {

      include mime.types;

      server {

        listen 80;
        server_name 167.99.93.26;

        root /sites/demo;

        index index.php index.html;

        location / {
          try_files $uri $uri/ =404;
        }

        location ~\.php$ {
          # Pass php requests to the php-fpm service (fastcgi)
          include fastcgi.conf;
          fastcgi_pass unix:/run/php/php7.1-fpm.sock;
        }

        location ~* \.(css|js|jpg|png)$ {
          access_log off;
          add_header Cache-Control public;
          add_header Pragma public;
          add_header Vary Accept-Encoding;
          expires 1M;
        }

      }
    }
    ```
  <p align="center"><img src="images/nginx_expires_request.png" width="800px"></p>

#

**Compressed Responses with gzip**

  
