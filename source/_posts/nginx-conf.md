---
title: Getting started with Nginx configuration
date: 2016-05-21 22:28:13
tags:
---
## Lets dive a little deeper

When it comes to configuring servers and provisioning them it really becomes a pain in the ass if we don't understand what's happening under the hood. Sometimes a configuration would work and sometimes it wouldn't. The reason for all these problems boils down to poor understanding of the directives that are used for configuration and not taking effort to read the documentation and researching on some of the best practices that need to be used. So lets dive a little deeper and experiment with Nginx configuration.

<!-- more -->

## TRY_FILES

A very common try_files line which can be applied on your condition is
```sh
location / {
	try_files $uri $uri/ /test/index.html;
}
```

You probably understand the first part, location / matches all locations, unless it's matched by a more specific location, like location	/test for example. The second part ( the try_files ) means when you receive a URI that's matched by this block try $uri first, for example http://example.com/images/image.jpg nginx will try to check if there's a file inside /images called image.jpg if found it will serve it first.

Second condition is $uri/ which means if you didn't find the first condition $uri try the URI as a directory, for example http://example.com/images/ , ngixn will first check if a file called images exists then it wont find it, then goes to second check $uri/ and see if there's a directory called images exists then it will try serving it. If there is no images directory it will retort to the third fallback option.

If there exists a directory called images and there is a index directive defined the nginx will try to check if the index exists inside this folder. For example if index is defined as index	index.html	index.htm then first nginx will try to serve the index.html file inside the images folder. If not present then it will try to serve the index.htm file inside the images folder. If none of the files listed in index directive is found or if the index directive was not at all present, then nginx will try to do a directory listing for the images folder. Now by default auto index is turned off in nginx, meaning directory listen must not be allowed. Therefore if we don’t set auto index as on explicitly using autoindex on you'll probably get a 403 forbidden error, because directory listing is forbidden by default. It is a good practise to leave auto index as off because it can expose contents present under the document root.

If there is no images directory then the third condition /test/index.html is considered a fall back option, (you need to use at least 2 options, one and a fall back), you can use as much as you can (never read of a constriction before), nginx will look for the file index.html inside the folder test and serve it if it exists. If the third condition fails too, then nginx will serve the 404 error page.

So the basic ﬂow is as follows 
- Tries to server the static ﬁle directly
- Checks if there is a folder in the given name of uri 
- If folder is present and index directive is there nginx tries to serve the index ﬁles in the folder 
- If no folder exists or there are no index ﬁles in the folder then tries to do a directory listing
- If there is no auto index directive we get a 403 forbidden error
- If auto index index is turned on explicitly using autoindex on then nginx does a directory listing. 

Also there's something called named locations, like this
```sh
location @error	{ }
```
You can call it with try_files like this
```sh 
try_files $uri $uri/ @error;
```
TIP: If you only have 1 condition you want to serve, like for example inside folder images you only want to either serve the image or go to 404 error, you can write a line like this
```sh
location /images { try_files $uri =404; }
```
which means either serve the ﬁle or serve a 404 error, you can't use only $uri by it self without =404 because you need to have a fallback option. You can also choose which ever error code you want, like for example:
```sh
location /images { try_files $uri =403; }
```
This will show a forbidden error if the image doesn't exist, or if you use 500 it will show server error, etc ..

## SERVER_BLOCK
Consider the following ﬁle /etc/nginx/sites-available/default Nginx can have diﬀerent server blocks. Each server block is wrapped within server { }
```sh
server	{
... }

server	{
... }

server	{
... }
```
The above file for example contains 3 server blocks. Different server blocks is what allows nginx to server different sites from the same server. When a HTTP request comes to nginx it first identifies the host and the port from the request headers. One of the headers in the request usually contains the host information. If a header is  ‘Host: example.com:8080’ then it means that the value of the Host header is example.com:8080. Therefore the host is example.com and the port is 8080. Once the host and port is identified by nginx it finds a matching  server block for the configurations. If there is not port then the implicit port 80 is used.
```sh
server	{	
	listen	80;				
	listen	[::]:80;				
	server_name	example.com	
	www.example.com;				
	... } 

server	{
	listen	80	default_server;
	listen	[::]:80	default_server;
	server_name	example.net;				
... }

server	{
	listen	80;				
	listen	[::]:80;
	server_name	example.app;
... }

server	{				
	listen	80;
	listen	[::]:80;
	server_name	"";
	return	444;
... }
```
Now with the above configuration a request with Host header as ‘Host: example.com’. The host is example.com and port is 80. Now to serve this request the first server block is used since that is the matching one. Now there can be possibilities where there is no matching server block, for example if the host header is ‘Host: example.org’, in these cases the server block having the default_server directive is used to process the request. So here in the above case the second server block would be used to serve the request. 

Now if there is no host header present at all in the request the matching server name is "". In the above case the 4th server block is used as it has the the server_name as "". If the fourth server_block was not defined above then in that case the server block having the default_server directive would be used.

Essentially whenever for a given host the matching server block is not found the server block having the default_server directive is used. And as you can see above a server block can have multiple server names, the first server block would be used to serve the request from both example.com and www.example.com on port 80. When we type http://example.com in our browser we are actually making a get request to the server with request header as ‘Host: example.com’ i.e host is example.com and port is 80.
```sh
server	{			
	listen	80	default_server;
	listen	[::]:80	default_server;
	root	/var/www/html;
	# Add index.php	to the list	if you are using PHP				
	index index.html index.htm index.nginx-debian.html;
	server_name	192.168.33.11;
	location / {
	try_files $uri $uri/ /cool/bro/file.txt;
	} 
}
```
If there is no default_server set on any server block then the first server block is used a the default server by nginx. Here there is only one server block and thus it automatically becomes the default one. But it is a good practice to state the default server block explicitly and thus we have use the default_server to indicate that this server block must be used in case there is no matching host found or in case there is no host header in the incoming request.