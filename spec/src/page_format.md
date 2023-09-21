# Page Format
- multipart (RFC 2046)
  - https://www.rfc-editor.org/rfc/rfc2046#section-5.1
- Content-Type: multipart/mixed
  - consumers SHOULD accept other multipart subtypes
  - "Applications must treat unrecognized subtypes as "multipart/mixed""
- are empty pages possible?
  - RFC: no
  - need some sort of note on that
- consumers SHOULD support LF in addition to CRLF
