---
title: Getting started with Nginx configuration
date: 2016-05-21 22:28:13
tags:
---
## TRY_FILES
A very common try_files line which can be applied on your condition is
```sh
location / {
	try_files	$uri	$uri/	/test/index.html;
}
```

You probably understand the first part, location	/ matches all locations, unless
it's matched by a more specific location, like location	/test for example. The second part ( the try_files ) means when you receive a URI that's matched by this block try $uri first, for example http://example.com/images/image.jpg nginx will try to check if there's a file inside /images called image.jpg if found it will serve it first.

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
location	@error	{ }
```
You can call it with try_files like this
```sh try_files	$uri	$uri/	@error;
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