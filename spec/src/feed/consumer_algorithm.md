# Consumer Algorithm
- crawl back via timestamp
- walk forward:
  - skip everything older than timestamp
  - with content ID: first entity after content ID -> exactly once semantics
  - without content ID: first entity with given timestamp -> at least once semantics
- forward-crawling via page timestamps as an optimization is allowed
  - but probably not that useful?

- consumers SHOULD report errors:
  - missing content ID
  - timestamps not old enough

- musings on different entry points?
