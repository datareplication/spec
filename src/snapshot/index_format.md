# Snapshot Index Format
The snapshot index, structured as a JSON document, is delivered over HTTP with the content type `application/json`. 
All linked pages within the index must contain absolute URLs.

## JSON Schema

```json
{{#include index.schema.json}}
```
It is allowed to include additional properties.

## Example of the snapshot index format
```json
{{#include index.example.json}}
```
