# Feed
A feed consists of a doubly-linked list of pages.
Each page usually has three `Link` HTTP page headers:
- self: url of the current page itself
- prev: url of the previous page
- next: url of the next page
The first page of the feed does not have a prev link. Also, the last page does not have a next link. 
You can find further information in the RFC 8288 (https://httpwg.org/specs/rfc8288.html#header).

Each page contains one of more entities. [Page Format](./page_format.md)

Each entity must have a Last-Modified header. They must be formatted using the timestamp format for HTTP `Last-Modified` Headers.
The must be monotonically increasing across all pages.

A page must have a Last-Modified header. It must be monotonically increasing from first to last page.
They must adhere to the following rules:
- Monotonically increasing across all pages
- 
Entry point to the feed is an url to a feed page. 
Typically, this is the latest page.

- doubly-linked list of pages
  - must not contain loops
  - links must be consistent
    - page1: next=page2
    - page2: prev=page1
- entry point: URL to a feed page
  - SHOULD be latest page
  - others are possible
- required header for every page:
  - Last-Modified
  - Link rel=self ???
  - if previous page: Link rel=prev
  - if next page: Link rel=next
- required header for every entity:
  - Last-Modified
  - Operation-Type (PUT, DELETE, PATCH)
  - Content-ID
    - strictly required?
- MUST support GET and HEAD requests
- Last-Modified MUST be monotonically increasing across all pages
- Last-Modified of a page MUST be the Last-Modified of its last entity
  - softer: >= Last-Modified of its last entity, <= Last-Modified of the first entity on the next page, >= Last-Modified of the previous page
- Content-IDs MUST be unique within a feed
- pages MUST be immutable
  - exceptions:
    - removing prev link from an old page to incrementally GC old things
    - latest page (= no next link): append more entities
    - latest page: add next link to newer pages

> I've written down some less-obvious requirements for feed page linking. This is probably not exhaustive, but should cover the tricky points:
> * A feed is a doubly-linked list of pages.
> * Page links must be consistent, i.e. the prev and next links of adjacent pages must match.
> * The feed must not form a loop.
> * Pages must have a self link.
> * A page without a prev link / next link marks the oldest / latest end of the stream respectively. These may be the same page.
> * Timestamps of entities must be monotonically increasing.
> * The timestamp of a page must be the timestamp of the last entity on the page.
> * Every page that can be navigated to by following the links backwards or forwards must be considered published.
> * Published pages must not be modified, with the following exceptions:
>   - Appending entities to a page without a next link.
>   - Adding a next link to a page that didn't have one before.
>   - Removing a prev link from a page (which makes older pages unreachable and e.g. eligible for garbage collection).
> * The latest URL should point to a page without a next link, but it's not strictly speaking incorrect for the page at the latest URL to have a next link. However, pages reachable by following that next link are reachable by consumers and must be considered published.
