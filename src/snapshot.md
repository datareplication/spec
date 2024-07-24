# Snapshot Overview
This document outlines the structure of a snapshot, which is composed of a snapshot index and multiple pages. 
The snapshot index is detailed in [Snapshot Index Format](./snapshot/index_format.md) and serves as a directory of page URLs. 
Each page, as defined in [Page Format](./page_format.md), contains at least one or more entities.

## Required headers
Each snapshot page must include the following mandatory headers.

| Name           | Required | Example                                                      |
|----------------|----------|--------------------------------------------------------------|
| Content-Type   | yes      | <sup>Content-Type: multipart/mixed; boundary="rdm-bny"</sup> |
| Last-Modified  | yes      | <sup>Last-Modified: Mon, 27 Nov 2023 03:10:00 GMT</sup>      |
