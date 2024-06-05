# Page Format

Page bodies are formatted using the multipart media type as defined in RFC 2046: [https://www.rfc-editor.org/rfc/rfc2046#section-5.1]
Each entity on the page is a body part in the multipart document. 
The multipart subtype should be 'mixed' but consumers should accept all other subtypes.
According to RFC 2046, empty pages are not possible.