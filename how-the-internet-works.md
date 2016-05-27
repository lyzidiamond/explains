---
layout: blog
title: How the internet works
---

When your computer connects to the internet, it is given an **[IP address](https://en.wikipedia.org/wiki/IP_address)**. This address is a unique identifier for your device on the internet. Every device that joins the internet is assigned an IP address.

There are lots of different types of devices that are connected to the internet. Some of those devices are referred to as **[servers](https://en.wikipedia.org/wiki/Server_(computing))**. The sole purpose of servers is to be on the internet to receive **requests** from other devices and provide **responses** to those requests, sending back a **resource** if it was requested. When you go to a website, you are making a _request_ to a _server_ that interprets the request and sends your browser a _response_ with the requested _resource_.

## Requests

### How requests are made

There are many ways to make requests, but the most typical is by using your browser. Requests can also be made using a command line utility called [`cURL`](https://curl.haxx.se/) or through other programs and libraries created specifically for making requests -- any technique for making requests is called the *[client](https://en.wikipedia.org/wiki/Client_(computing))*.

### HTTP

Most requests that users make on the internet use the **[HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)** scheme. HTTP stands for _hypertext transfer protocol_ and is the main scheme used by the world wide web for sending requests and responses. (You may also be familiar with **[FTP (file transfer protocol)](https://en.wikipedia.org/wiki/File_Transfer_Protocol)**.) HTTP defines a set of common types of requests and responses that can be interpreted by all devices. Requests made over HTTP are prepended by `http://` or `https://`.

### Request structure

HTTP requests, like websites, contain a `head` and a `body`. The `head` contains meta information about the request, and the `body` contains a resource or resources intended to accompany the request. Whether or not a `body` is sent depends on the type of request. HTTP servers are programmed to respond to different types of requests.

The `head` of the request is required and includes a couple important pieces of information: the **[request method](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)** and a **resource** (often in the form of a **URL**). There are several other headers that are included with a request, but they are for the most part included by the client.

#### Request methods

Common request methods include:

- `GET`: this is the most common request when accessing a website with your browser. A `GET` request method indicates that the client is requesting some resource from the server, but is not sending any resources along with the request.
  - Example: typing www.facebook.com into your browser and pressing enter. You are requesting the Facebook webpage.
- `POST`: sends a request along with a resource to be posted to the server.
  - Example: making a Facebook status update and pressing submit. The status update is sent as the `body` of the request.
- `DELETE`: sends a request to delete a resource on the server.
  - Example: deleting a Facebook status update.
- `PUT`: this method sends a request to post something to the server; if there is already something at the specified location, it is modified.
  - Example: editing a Facebook status update. The new status update is sent as the `body` of the request.

When you type a URL into the browser and press enter, your browser makes a `GET` request to a server for a specific resource.

#### Resources

When you make a request, you are requesting some specific resource -- whether you want to retrieve something from that location, delete something from that location, or post something to that location, the resource identifies _where_ on the server you're making the request to.

Most of the time, the resource you're requesting will be in the form of a **[URL](https://en.wikipedia.org/wiki/Uniform_Resource_Locator)**. URL stands for _uniform resource locator_ and is a human-readable way to identify resources hosted on a server. The URL is broken into a few parts:

`https://hostname:port/path-or-endpoint/resource?query=parameter`

- **hostname:port**: this is the main location of the server. When you type a URL into the browser and press enter (or use any other client), the URL is translated to an IP address using **[DNS (domain name system)](https://en.wikipedia.org/wiki/Domain_Name_System)**, which is like a phone book for domain names, and the request is routed to the correct device (most typically a server). When that server is identified, the client establishes a connection with the server that is listening for request (this is called an HTTP server). The HTTP server then interprets the request, usually by routing it to the code related to the specificed **endpoint**. (Note: most of the time, the _port_ is not explicitly defined and instead is handled by the server.)
- **path-or-endpoint**: once on the server, this is where to look for the resource. In the case of web pages, this is considered to be a _path_. When engaging with an API, it is often called an **endpoint** (see below for more information on APIs).
- **resource**: the actual resource being requested. This can be a webpage (like `index.html`), an image (like `puppies.jpg`), or some other resource.
- **query=parameter**: query parameters allow you to send additional information along with the request. Sometimes this provides more information for the server to better respond to the request.

#### Request body

With a `POST` or `PUT` request, you can send a resource along with the request in the **[request body](https://en.wikipedia.org/wiki/HTTP_message_body)**. Usually this is for adding a resource to the database on the server, like the example above of adding a Facebook status update.

### How a server handles the request

A server is a computer that is connected to the internet (so it has an IP address) that has one or more _ports_ that are listening for HTTP requests. The server has code on it that is programmed to respond differently to different types of requests depending on the type of request, the URL of the request, and the request body.

## Responses

Once the server receives a request, it has to interpret the request and provide the appropriate **response**. Responses include a **status code** and sometimes a **resource** or resources (depending on the request).

### Status codes

Every HTTP request receives a response, whether it's successful or not. **[HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)** are pre-defined responses that dictate what is happening with the request and/or how the request went.

There are five groups of HTTP status codes:

- `1xx`: informational; request is still going through, just wanna tell you what's going on
- `2xx`: success; the request went through without a hitch
- `3xx`: redirection; the request needs to be redirected, but nothing has gone wrong
- `4xx`: client error; the request cannot be fulfilled because of user/client error
- `5xx`: server error; the request looks fine, but something's going on on the server side and the request can't be fulfilled

Status codes can provide a lot of information about what's going on with your code and application. For a full list of HTTP status codes with cute pictures of puppies, see [HTTP status dogs](https://httpstatusdogs.com/). (For the cat fans, there is also [HTTP status cats](https://http.cat/).)

Common HTTP status codes include:

- `200 OK`: Success! Everything worked out just fine.
- `404 Not Found`: there is nothing at the location of the request (you probably typed the URL wrong).
- `503 Service Unavailable`: the server barfed; this is common when a website is receiving lots and lots of traffic and goes down.

### Resources

Some successful requests result in resources being sent back to the client. This is not true of every request, but many requests yield responses with resources. Responses, just like requests, have a `head` and a `body`. The status code of the response is included in the response `head`, and the resource (if any) is included in the response `body`.

The structure of the resource is defined by the server that is serving it and can be nearly anything, from HTML pages to images to JavaScript and CSS files.

### How to receive responses

If you type a URL into a browser window and press enter, you are making a `GET` request for whatever resource is at the other end of that URL. Most of the time this is a HTML webpage. In this case, the server interprets the request, and returns the HTML page to be displayed in your browser.

HTML pages tend to also require a bunch of other resources besides the HTML page itself, including JavaScript and CSS files, images, fonts, content from databases, and much more. Once the HTML page is returned to the browser, the browser reads through it and makes requests for everything that is listed in the `head` and `body` of the HTML page. As an example, to load `www.mapbox.com` requires nearly 100 individual HTTP requests, including SVGs like [turf.svg](https://www.mapbox.com/home/icons/turf.svg), JavaScript files like [base.js](https://www.mapbox.com/base.js/dist/base.js), fonts like OpenSans, and even [static map images](https://api.mapbox.com/styles/v1/mapbox/satellite-streets-v9/static/140.01,-21.24,3/800x500?access_token=pk.eyJ1IjoibXNsZWUiLCJhIjoiclpiTWV5SSJ9.P_h8r37vD8jpIH1A6i1VRg) from the Mapbox Static API.

One other very common way to receive responses is programmatically in a web or mobile application using a **[web API](https://en.wikipedia.org/wiki/Web_API)**. An excellent example of this is maps made with Mapbox tools: When you make a map with Mapbox.js or Mapbox GL JS, the JavaScript in your code makes a _request_ to the Mapbox servers for tiles and styles to load on the map, and the _response_ is interpreted by your code and passed into the map object to display on the page.

## Web APIs

**[API](https://en.wikipedia.org/wiki/Application_programming_interface)** stands for _application program interface_. Web APIs are a pre-defined list of URLs that are used to access specific resources on a server. APIs are often used to provide and manage access to resources located in a database, or used as a way to do processing tasks on a server instead of within an application or in the browser.

Mapbox APIs that provide and manage access to database resources:

- [Styles API](https://www.mapbox.com/api-documentation/#styles) - used to add, modify, and delete styles from your account; interacting with the database of Mapbox user data
- [Datasets API](https://www.mapbox.com/api-documentation/#datasets) - used to add, modify, and delete datasets from your account; interacting with the database of Mapbox user data

Mapbox APIs that do processing tasks:

- [Geocoding API](https://www.mapbox.com/api-documentation/#geocoding) - takes coordinates and runs through carmen (geocoder) to produce addresses (and vice versa)
- [Directions API](https://www.mapbox.com/api-documentation/#directions) - takes waypoints and runs through OSRM (routing engine) to produce directions

Mapbox APIs that do both:

- [Static API](https://www.mapbox.com/api-documentation/#static) - simultaneously interacts with database of Mapbox data to get styles and processes the style to create a static image
- [Uploads API](https://www.mapbox.com/api-documentation/#uploads) - simultaneously processes data to create tilesets and interacts with the database of Mapbox data to add the new tileset

### Access tokens and authentication

HTTP requests can have various types of authentication associated with them natively (built into the request process), and some servers also require separate types of authentication. In the case of Mapbox, we request authentication when accessing our APIs in the form of an **access token** which is appended to the request as a query parameter.

Authentication (in any form) is a way to track usage and prevent abuse. By authenticating, the user is providing their identity to the HTTP server, which allows the server to keep track of requests and responses per user to make sure that they are only accessing resources to which they should have access, to charge them for specific types of usage, or to collect statistical information.

### Using APIs

APIs are commonly used inside of web applications -- a resource is requested via an API and the application parses the response and plugs it into the appropriate place in the application. Mapbox Studio is a great example -- it is a web application that interacts with Mapbox APIs. When a user goes to the Styles page, Mapbox Studio makes a request to the Styles API to [retrieve a list of styles for the user](https://www.mapbox.com/api-documentation/#list-styles). When Mapbox Studio receives the list in the response (returned as a JSON object), the code in Mapbox Studio iterates through that list, parses each style, and makes an entry for it on the Styles page.

Nearly every programming language has native (built-in) methods for making HTTP requests, which makes API calls in applications fairly straightforward. Some tools also have **[SDKs (software development kits)](https://en.wikipedia.org/wiki/Software_development_kit)** or **[command-line tools](https://en.wikipedia.org/wiki/Command-line_interface)** with methods specifically for interacting with a specific API or a set of APIs. For example, Mapbox has a [command line interface](https://github.com/mapbox/mapbox-cli-py), a [Python SDK](https://github.com/mapbox/mapbox-sdk-py), a [JavaScript SDK](https://github.com/mapbox/mapbox-sdk-js), and more.

## Other useful topics and tools

- [Postman](https://www.getpostman.com/) is software for making and investigating API requests and responses that exposes what's going on behind the scenes.
- [REST (Representational State Transfer)](https://en.wikipedia.org/wiki/Representational_state_transfer) is the main architectural style for web APIs. It's a bit confusing, but can be useful information.
- [what-happens-when](https://github.com/alex/what-happens-when) is a project that explains how the internet works in way way way more detail than I went into here. It is open source and collaborative.
- [How Does The Internet Work?](https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm) is a white paper from Russ Shuler at Stanford about (yes you guessed it) how the internet works. Much of the same content covered here, but much more detail and slightly different descriptions (and certainly far fewer Mapbox examples).
- [How does the Internet work?](https://developer.mozilla.org/en-US/Learn/Common_questions/How_does_the_Internet_work) from the [Mozilla Developer Network](https://developer.mozilla.org/en-US/). MDN is generally a great resource for all things web dev.
