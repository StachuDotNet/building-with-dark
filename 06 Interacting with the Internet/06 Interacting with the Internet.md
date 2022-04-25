# [18] Working with the Internet


## [3] Handling Requests with HTTP Handlers

### Creating Endpoints, and Intro to the `HTTP::` module
- The `HTTP::` module provides functions to create responses to external HTTP calls.
- Each response function, such as HTTP::respond, creates a response value
	- a response value returned by the handler will be sent as a response to the client

### Reading the Http Request
- get head, body, etc.
- reading the Request
	- expose Request type to user?

### Returning Http Responses

#### Positive
- `::success`

#### Neutral
- `::setCookie`
- `::redirectTo`
- `::response`
	- `::responseWithHeaders`
	- `::responseWithHtml`
	- `::responseWithJson`
	- `::responseWithText`

#### Negative
- `::forbidden`
- `::badRequest`
- `::notFound`
- `::unauthorized`

#### ?
- set status code
- set http headers 
	is this the same as with HttpClient? some shared stuff?



## Making requests (with `HttpClient::_v5`)
### making requests
all of ^ take 3-4 params: uri, query, body, and header
	- `::get`
	- `::post`
	- `::options`
	- `::delete`
	- `::put`
	- `::patch`
	- `::head`

### Setting HTTP Headers
- There are built-in header fns for commonly used headers, including authentication (`::basicAuth`, `::BearerToken`) and content types for plain text, JSON, HTML, and forms. Headers are dictionaries; to combine two headers, use Dict.merge
- auth
	- `::basicAuth`
	- `::bearerToken`
- setting content types
	- `::plainTextContentType`
	- `::formContentType`
	- `::jsonContentType`
	- `::htmlContentType`


## HTTP Packages
- show all at high level (intention, types, fns, examples, future)
- twilio
- asana
- slack
	- mention slack use case and demo etc
- stripe

## Static Assets
(see adjacent doc)

## JWT
- what's a jwt? usage
- `::signAndEncodeWithHeaders`
- `::signAndEncode`
- `::verifyAndExtract`
- some demos


## Custom Domains
- what's this for?
- normally hosted on bwdserver.com
- what we do/don't support (subdomain vs toplevel domain)
- current manual process
future UI-based process

## CORS
- what is it
- what's our part?