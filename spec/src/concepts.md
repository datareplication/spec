# Concepts

All information is served over HTTP. 
Every request must ultimately have the HTTP status code 200 except for if there is an error to report. 
If there is an error to report the status code will be within 4xx or 5xx according to the error case.
The data served over HTTP consists of two main concepts: entities and pages.

- things delivered over HTTP
  - everything must ultimately be 200
  - 4xx, 5xx can be considered errors to report
  
## Entities
Entities are the smallest logical unit. They represent the model of information to provide. 
They consist of any number of headers and a body of arbitrary bytes. 
Headers and body can be thought of as similar to HTTP response headers and HTTP response body respectively.

## Pages
A page consists of one or more entities. 
It is referenced by a unique url and served over HTTP. Much like an entity, a page has headers and a body. 
They are the headers and body of the HTTP response. The format of the page body is documented separately: [Page Format].
