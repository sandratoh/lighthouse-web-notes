# HTTP Introduction

## What is HyperText?

> Hypertext is text which contains links to other texts.

* HyperText is the `HT` in `HTTP` AND `HTML`
* Its origins date back to the 1960's

## HTTP Intro

* HTTP is a protocol used to read and write 'resources' (data) in a simple text-based manner
* Started off mostly for HTML docs, but now it's used in all sorts of doc
  * E.g: JS files, CSS, PDFs, etc.


## HTTP Flow - Request-Response Based

* Client makes request to an HTTP server
* Immediately after that, client also sends a message asking for specific resource
* Server sends down the message as a response
* Server cannot send response to client if client has not first sent a request

### MDN Notes

#### HTTP Flow
1. Open a TCP Connection: used to send request(s) and receive answer(s).

2. Send an HTTP message (more next section):
  * Before HTTP/2 - messages are human-readable
  * HTTP/2 - encapsulate messages in frames so no longer able to read directly

3. Read response sent by the server

4. Close or reuse the connection for further request

Note: If HTTP pipelining is activated, several requests can be sent before first repsonse is fully received.

#### HTTP Messages
* HTTP/1.1 and earlier: human-readable
* In HTTP/2: messages embbed into a binary structure, a *frame*, so as to allow message optimizations
* Two types of HTTP messages:
  1. **Requests**:  
      * An HTTP `method` that defines the operation the client wants to perform. (eg: a verb like `GET`, `POST`, or a noun like `OPTIONS`  OR `HEAD`)
      * Path of the resource to fetch
      * The version of the HTTP protocol
      * Optional headers that convey additional info for the server
      * A body, for some methods like `POST`, similar to those in responses, which contain the resource sent.

  2. **Responses**:
      * Versions of the HTTP protocol they follow
      * A status code, indicating if the request was successful, or not, and why
      * A status message, a non-authoritative short description of the status code
      * HTTP headers, like those of requests
      * Optionally, a body containing the fetched resource

## HTTP Methods
There are 9 HTTP request methods (aka *verbs*), but just need to know 4 right now:

* `GET`: to 'get' some data from the server
* `POST`: usually for creating some new data
* `PUT`: generally for editing existing data on the server
* `DELETE`: to delete some existing data

## Paths and URL Structures
* Need to know the URL (*Uniform Resource Locator*) of an HTTP server in order to request a 'resource'.
* Path is part of the URL

### MDN Notes

* URL - mechanism used by browsers to retrieve resources on the web. It is the address of a given unique resource on the Web.

```
http://www.example.com:80/path/to/myfile.html/?key1=value1&key2=value2#SomewhereInTheDocument
```

* Protocol/Scheme - (`http`)
  * first part of the URL
  * indicates the protocol the browser must use to request the resource
  * Usually `https` (secured) or `http` (unsecured) for websites
  * Other schemes:
    * `mailto:` to open a mail client
    * `ftp:` to handle file transfer

* Authority - separated from scheme by the character path `://` (*colon separates scheme from next part of URL; `//` indicates next part is authority*)

  * Domain (or Host) - (`www.example.com`)
    * indicates which web server is being requested
    * can be domain name or IP address

  * Port - (`80`)
    * indicates the technical 'gate' used to access the resources on the web server
    * usually omitted if server uses standard ports of the HTTP protocol to grant access to its resources, otherwise it's mandatory
      * HTTP = 80
      * HTTPS = 443

* Resource Path - (`/pathtomyfile.html`)
  * used to be physicle file location on the web server
  * now mostly an abstraction handled web server without any physical reality

* Query Parameters - (`?key1=value1&key2=value2`)
  * list of key/value pairs separated with the `&` symbol
  * Web server can use those parameters to do extra stuff before returning the resource
  * Each server has own rules regarding parameters

* Anchor - (`#SomewhereInTheDocument`)
  * anchor to another part of the resource itself
  * like a 'bookmark' inside the resource
  * Eg: in HTML, a certain section of the page
  * Eg: in video doc, a certain time in the vid
  * the part after the `#` is the **fragment identifier**, it's never sent to the server with the request

## HTTP Responses

Just looking into **status code** and **body** for now.

### HTTP Status Codes

* how a server relay info to a client

* 3 digit number the server puts in response to let client know whether user operation was successful

* Some useful status codes to know
  * `200`: 'Everything went great!'
  * `201`: 'The request has successed and a new resource has been created as a result.'
  * `404`: 'Resource was not found.'
  * `500`: 'The server had an error.'

### Response Body

* Responses usually contain some data like the ones the client originally requested - those data gets stored into `body` of the response
* Can store data in many kinds of format

## Headers

* A key-value way of storing data (extra info) in a request or response

## Conclusion
* HTTP is a request-respones protocol, where the client makes requests and the server sends responses

* HTTP is a text based protocol, making it easy to read and understand for humans

* HTTP requests must contain the verb/method and the Path

* HTTP requests aren't always to receive data, but sometimes to save data

* Requests and responses both contain key-value based headers