---
title: Network requests with NSURLSession
date: 2016-07-20 15:17:32
tags:
---
## HTTP Requests
We are living in world today where information is being rapidly exchanged between every device that we use. Almost every application on the market these days consume content through a web service. While Alamofire is a rich networking library that can be used to access APIs, you can also use NSURLSessions’s asynchronous data task requests for quick and dirty REST calls. Infact Alamofire library is nothing but a wrapper around NSURLSession written in Swift that simplifies making HTTP requests.

<!-- more -->

## So where do we start ?
* Apple has introduced App Transport Security(ATS) in iOS 9. ATS requires SSL to be used for transferring data and it is pretty picky about how it’s implemented. Sadly this means that a lot of servers out there don’t meet the ATS requirements. So what can we do if we need to work with one of these servers? We’ll have to add an exception to App Transport Security for that server.
* While we could just disable ATS itself, but it’s much more secure to create an exception only for the one server that we need to access which is not ATS compliant. The API that we’ll be using in this chapter is at http://jsonplaceholder.typicode.com/ so that’s what we’ll create the exception for.
* To create the exception we’ll need to add some keys to the info.plist in our project. We’ll add a new row and select App Transport Security Settings from the drop down. That will create a dictionary for us. Then we’ll click the + sign to add a row to the dictionary and choose Exception Domains. And add a row in that dictionary. Change the new row to a dictionary and change its name to jsonplaceholder.typicode.com (note: no trailing slashes and no http or https prefix). Within the jsonplaceholder.typicode.com dictionary, add a single boolean entry NSThirdPartyExceptionAllowsInsecureHTTPLoads set to YES
* JSONPlaceholder is a fake online REST API for testing and prototyping. You can check it out at http://jsonplaceholder.typicode.com
* First step would be to create a NSURL instance of the endpoint
* Then we need to create a NSURLRequest object with the url object
* Create a session object to create a task to send the request
* Create a task to send the request from the session object
* Start the task to actually send the http request
* Now once we get the response the callback that we gave will be executed, make sure we got data and no error
* Try to transform the data into JSON (since that’s the format returned by the API)
* Access the todo object in the JSON and print out the title
* The default request is a GET request, to make a different kind of HTTP request we create a NSMutableRequest and set the HTTPMethod & HTTPBody appropriately
```swift
func makeGetRequest() {
    if let url = NSURL(string: "http://jsonplaceholder.typicode.com/todos/1") {
        
        let request = NSURLRequest(URL: url)
        let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration())
        
        let task = session.dataTaskWithRequest(request, completionHandler: { data, response, error in
            if let responseError = error {
                print("Error calling GET on /todos/1")
                print(responseError)
            }
            
            if let responseData = data {
                do {
                    if let todo = try NSJSONSerialization.JSONObjectWithData(responseData, options: []) as? [String: AnyObject] {
                        if let title = todo["title"] {
                            if let name = title as? String {
                                print(name)
                            } else {
                                print("The title could not be converted to a string")
                            }
                        } else {
                            print("There was not title in the dictionary")
                        }
                        
                    } else {
                        print("Unable to convert the data to JSON")
                    }
                } catch {
                    print("Unable to convert the data to JSON")
                }
            }
        })
        task.resume()
        
    } else {
        print("The url is not a valid one")
    }
}

func makePostRequest() {
    if let url = NSURL(string: "http://jsonplaceholder.typicode.com/todos") {
        
        let request = NSMutableURLRequest(URL: url)
        request.HTTPMethod = "POST"
        let newTodo = ["title": "Frist todo", "completed": false, "userId": 1]
        do {
            let jsonData = try NSJSONSerialization.dataWithJSONObject(newTodo, options: [])
            request.HTTPBody = jsonData
            
            let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration())
            
            let task = session.dataTaskWithRequest(request, completionHandler: { data, response, error in
                if let responseError = error {
                    print("Error calling GET on /todos/1")
                    print(responseError)
                }
                
                if let responseData = data {
                    do {
                        if let todo = try NSJSONSerialization.JSONObjectWithData(responseData, options: []) as? [String: AnyObject] {
                            if let id = todo["id"] {
                                if let identifier = id as? Int {
                                    print(identifier)
                                } else {
                                    print("The identifier could not be converted to a integer")
                                }
                            } else {
                                print("There was not identifier in the dictionary")
                            }
                            
                        } else {
                            print("Unable to convert the data to JSON")
                        }
                    } catch {
                        print("Unable to convert the data to JSON")
                    }
                }
            })
            task.resume()

        } catch {
            print("Cannot create data from JSON object")
        }
    } else {
        print("The url is not a valid one")
    }
}
```