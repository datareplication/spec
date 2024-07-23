# Feed
A feed is a sequence of entities that chronicle modifications to a resource, organized into multiple pages. 
Each page contains at least one or more entities.

Typically, a page in a feed includes three `Link` HTTP headers:
- `self`: the URL of the current page
- `prev`: the URL of the preceding page
- `next`: the URL of the subsequent page
> **_NOTE:_** The initial page lacks a `prev` link, and the final page omits a `next` link. 
Additional details on this can be found in [RFC 8288](https://httpwg.org/specs/rfc8288.html#header).

Refer to [Page Format](./page_format.md) for the structure of each page, which accommodates one or more entities.

## Required headers
There are some required headers for every page.
For a feed page, the `Link; rel=next` and `Link; rel=prev` header is optional.

| Name           | Required | Example                                                      |
|----------------|----------|--------------------------------------------------------------|
| Content-Type   | yes      | <sup>Content-Type: multipart/mixed; boundary="rdm-bny"</sup> |
| Last-Modified  | yes      | <sup>Last-Modified: Mon, 27 Nov 2023 03:10:00 GMT</sup>      |
| Link; rel=self | yes      | <sup>Link: https://example.com/feed/hash;rel=self</sup>      |
| Link; rel=next | no       | <sup>Link: https://example.com/feed/hash;rel=next</sup>      |
| Link; rel=prev | no       | <sup>Link: https://example.com/feed/hash;rel=prev</sup>      |


### Last-Modified
Each entity must have a Last-Modified header. They must be formatted using the timestamp format for HTTP `Last-Modified` Headers.
> **_NOTE:_** The must be monotonically increasing across all pages.

> **_NOTE:_** Links must be consistent, i.e. the prev and next links of adjacent pages must match and the feed must not form a loop.

## Finding an entry point
Each feed consumer needs to find a valid starting point.
This can be determined reading the feed from the beginning or by using a snapshot as a starting point. 
The snapshot's creation date serves as the entry point. 

## Resume consumption
After fully consuming the feed, it's important for the consumer to note the `Last-Modified` date of the last entity. 
This date then becomes the new entry point for future consumption. 
Additionally, to avoid processing the same entity multiple times, consumers are advised to record the `Content-ID` of the last entity they processed.

## Pagination
To ensure efficient navigation and access for feed consumers, it's essential for providers to incorporate pagination mechanisms. 
This process involves crawling to the feed through both `HEAD` requests and `GET` requests for retrieving specific pages.

## Immutability of pages
Treat published pages as immutable once created, with a few specific exceptions:
- New entities can be added to the most recent page if it doesn't have a `next` link.
- A `next` link can be introduced to the most recent page, after which it becomes immutable.
- A `prev` link may be removed from an older page as part of a gradual cleanup process.
