# Concepts
Information is transmitted exclusively via HTTP. 
Each request should result in an HTTP status code of 200, unless an error occurs, 
in which case the status code will fall within the 4xx or 5xx range, depending on the nature of the error.

The data served over HTTP consists of two main concepts: [Snapshots](./snapshot.md) and [Feeds](./feed.md).
