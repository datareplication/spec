# Snapshot Index Format
The snapshot index is a JSON document. It is served over HTTP with the content type `application/json`. Page urls must be absolute.

## JSON Schema

```json
{{#include index.schema.json}}
```
It is allowed to include additional properties.

## Example of the snapshot index format
```json
{{#include index.example.json}}
```
