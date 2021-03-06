# nginx-Guide

Check that process is running 
<pre>ps aux | grep nginx</pre>

Update ubuntu apt package manager
<pre>apt-get update</pre>

# Configuration 

The two main configuration terms are 
1. Context 
    - A section within a configuration - It's the same as scope. 
2. Directive
    - Specific configuration options that get's set in in the configuration files, it consists of a name and a value.

Download configuration
<pre>wget http://nginx.org/download/nginx-1.21.5.tar.gz</pre>

unpackage
<pre>tar -zxvf nginx-1.21.5.tar.gz</pre>

Full confuguration source
<pre>./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module</pre>

## Creating A Virtual Host
##### Example 
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/01%2BCreating%2Ba%2BVirtual%2BHost.conf

## Location (context)
It's used for defining behaviour for specific uri or requests. 

Prefix match is a match that matches anything "starting" with. 
Example of custom location context (prefix match)
<pre>
		location /greet {
			return 200 'Hello from NGXI greet location!';
		}
</pre>


Exact match is when it matches only the exact uri. this is done with
<pre>location = /greet {... }</pre>

Regex match is when uri includes a regex for a broader match. Regex match is case sensative.
<pre>location ~* /greet[0-9] { ... }</pre>

##### Example

https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/02%2BLocation%2BBlocks.conf

## Variables
http://nginx.org/en/docs/varindex.html

https://www.nginx.com/resources/wiki/start/topics/depth/ifisevil/

These are all the native nginx variables
http://nginx.org/en/docs/varindex.html

Example of how to make conditition in conf file using variables 
<pre>
    if ( $arg_apikey != 1234) {
        return 401 "Incorrect API key!
    }
</pre>

##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/03%2BVariables.conf

### Create your own variable
<pre>set $weekend 'No';</pre>

## Rewrites & Redirects
https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

- Rewrites rewrites the uri internally 

- Redirects redirects the user based on a uri.

##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/04%2BRewrites%2B%26%2BRedirects.conf

## Try Files & Named Locations 
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/05%2BTry%2BFiles%2B%26%2BNamed%2BLocations.conf

### try_files
It's a directive that enables us to check of vailable uri paths and foces a redirect to that uri path if it exists.
## Logging 
http://nginx.org/en/docs/ngx_core_module.html#error_log

http://nginx.org/en/docs/http/ngx_http_log_module.html

https://docs.nginx.com/nginx/admin-guide/monitoring/logging/

##### Example 
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/06%2BLogging.conf

### access_log
It's a directive that can be put inside of contexts to log specific location (uri) accesses etc.

This enables us to personalize logging very much for different kinds of access to paths.


## Inheritance and directives
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/07%2BInheritince%2B%26%2BDirective%2BTypes.conf

## PHP Processing
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/08%2BPHP%2BProcessing.conf
## Worker Processing
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/09%2BWorker%2BProcesses.conf

## Buffers & Timeouts
http://nginx.org/en/docs/syntax.html

##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/10%2BBuffers%2B%26%2BTimeouts.conf

## Dynamic modules
http://nginx.org/en/docs/http/ngx_http_image_filter_module.html

##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/11%2BAdding%2BDynamic%2BModules.conf

# Performance
## Headers & Expires
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/12%2BHeaders%2B%26%2BExpires.conf

## Compressed Responses with gzip
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/13%2BCompressed%2BResponses%2Bwith%2Bgzip.conf

## FastCGI Cache
http://nginx.org/en/docs/http/ngx_http_fastcgi_module.html

https://httpd.apache.org/docs/2.4/programs/ab.html
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/14%2BFastCGI%2BCache.conf

## HTTP2
https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-16-04
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/15%2BHTTP2.conf

## Server Push 
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/16%2BServer%2BPush.conf

# Security
## HTTPS (SSL)
Links:
https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange 

https://hackernoon.com/algorithms-explained-diffie-hellman-1034210d5100

##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/17%2BHTTPS%2B(SSL).conf
## Rate Limiting
- Security 
- Reliability 
- Shaping

##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/18%2BRate%2BLimiting.conf

## Basic Auth 
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/19%2BBasic%2BAuth.conf

# Hardning Nginx
- Disable IFrame availability
- Block cross site scripting
##### Example
https://github.com/KristoferMar/nginx-Guide/blob/main/Examples/20%2BHardening%2BNginx.conf

## SSH
Good to know: 
- "Let's encrypt" and other providers dont provide certificates for ip adresses - Only valid url domains.
## Install Certificate
https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal


Remove known host
<pre>ssh-keygen -R hostnameOrIp</pre>


# Reverse Proxy & Load Balancing
## Prerequisites
https://gist.github.com/willurd/5720255 

https://www.php.net/manual/en/features.commandline.webserver.php

## Reverse Proxy
https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/

http://nginx.org/en/docs/http/ngx_http_proxy_module.html

## Load Balancer
A load balancer recognceses any kind of error within a server and distributes the trafic to another working server instead.

- The upstream context is used to configure loadbalancing between servers.

http://nginx.org/en/docs/http/load_balancing.html

https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/

http://nginx.org/en/docs/http/ngx_http_upstream_module.html