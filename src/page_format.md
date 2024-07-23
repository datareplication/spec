# Page format
Pages utilize the multipart media type for formatting, as specified in [RFC 2046](https://www.rfc-editor.org/rfc/rfc2046#section-5.1).

To differentiate between entities within a multipart document, a `Content-Type` header specifying a boundary is required: `multipart/mixed; boundary="<random-boundary>"`. 
This boundary, a unique string not found in the content, separates each entity.

> **_NOTE:_** According to RFC 2046, empty pages are not possible.

## Required and optional entity headers
Each entity within a page must include specific headers.

| Name           | Snapshot | Feed | Example                                                 |
|----------------|----------|------|---------------------------------------------------------|
| Content-Type   | yes      | yes  | <sup>Content-Type: text/plain</sup>                     |
| Last-Modified  | yes      | yes  | <sup>Last-Modified: Mon, 27 Nov 2023 03:10:00 GMT</sup> |
| Content-Length | yes      | yes  | <sup>Content-Length: 42</sup>                           |
| Content-ID     | no       | yes  | <sup>Content-ID: a-random-content-id-or-hash</sup>      |
| Operation-Type | no       | yes  | <sup>Operation-Type: http-equiv=PUT</sup>               |

### Content-ID
The `Content-ID` header is used to uniquely identify an entity within a feed. 
It is required for every feed entity and must be unique within a feed.

### Operation-Type
The `Operation-Type` header is used to indicate the operation that was performed on the entity.
Possible values are: `PUT`, `DELETE`, `PATCH`.

## Examples:
Snapshot page:
```multipart
{{#include page/snapshot.content.multipart}}
```
Feed page:
```multipart
{{#include page/feed.content.multipart}}
```


