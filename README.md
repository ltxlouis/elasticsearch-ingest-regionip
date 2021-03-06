# Elasticsearch regionip Ingest Processor

#### supported Elasticsearch verison: 6.2.4
Uses the [ip2region](https://github.com/lionsoul2014/ip2region) lib to add Chinese region info based on provided ip address

## Installation
1. download .zip file
2. use Elasticsearch elasticsearch-plugin command to install locally
[[reference]](https://www.elastic.co/guide/en/elasticsearch/plugins/6.2/plugin-management-custom-url.html)

## Usage

```
PUT _ingest/pipeline/custom-pipeline-name
{
  "description": "custom description",
  "processors": [
    {
      "regionip": {
        "field": "field_containing_ip_address",
        "target_field": "target_field_name",
        "properties": ["country_name", "region_name", "city_name"]
      }
    }
  ]
}
```

```
target_field result example

"regionip": {
  "country_name": "中国",
  "city_name": "上海市",
  "region_name": "上海"
}
```

##### for more usage please refer to official [doc](https://www.elastic.co/guide/en/elasticsearch/reference/6.2/ingest.html)

## Configuration

| conf | required | note |
| --- | --- | --- |
| field          | yes | Field name containing ip address |
| target_field   | no | Field name to write region info to, defaults to `regionip` |
| ignore_missing | no | If set to true, doc missing specified field will not throw a exception, defaults to `false`. |
| ip2region_algorithm | no |`BTREE`/`BINARY`/`MEMORY`, defaults to `MEMORY` [[link]](https://github.com/lionsoul2014/ip2region) |
| properties | no | `ip`, `country_name`, `region_name`, `city_name`, `isp_name`, defaults to all properties |

## Build

```bash
gradle clean assemble
```
