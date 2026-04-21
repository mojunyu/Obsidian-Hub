


``` sql
# 查询 request_body 里 event_name、conversion_type、event_type 都不等于 install 或 reinstall的数据

{
  "bool": {
    "must_not": [
      { "terms": { "event_name": ["install", "reinstall"] } },
      { "terms": { "conversion_type": ["install", "reinstall"] } },
      { "terms": { "event_type": ["install", "reinstall"] } }
    ]
  }
}

```