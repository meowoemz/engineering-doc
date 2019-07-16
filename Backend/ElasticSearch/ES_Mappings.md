# Create multiple types for ES index

```
{
   "data": {
      "mappings": {
         "people": {
            "properties": {
               "name": {
                  "type": "string",
               },
               "address": {
                  "type": "string"
               }
            }
         },
         "transactions": {
            "properties": {
               "timestamp": {
                  "type": "date",
                  "format": "strict_date_optional_time"
               },
               "message": {
                  "type": "string"
               }
            }
         }
      }
   }
}
```

If using ES php sdk client, need to add multiple types to current index.

if you want to search some field as array, for instance `restaurant_id`
`restaurant_id` field mapping is important here as it needs to be `not analyzed`.

```
$params = [
            'index' => $this->elasticsearch_index,
            'body' => [
                'mappings' => [
                    $this->elasticsearch_menu_type => [
                        '_source' => [
                            'enabled' => true
                        ],
                        'properties' => [
                            'id' => ['type' => 'string'],
                            'restaurant_id' => ['type' => 'string', "index" =>  "not_analyzed"],
                            'name' => ['type' => 'string'],
                            'price' => ['type' => 'float'],
                            'description' => ['type' => 'string'],
                            'categories' => ['type' => 'string'],
                            'start_time' => ['type' => 'date', 'format' => 'HH:mm:ss'],
                            'end_time' => ['type' => 'date', 'format' => 'HH:mm:ss'],
                            'discount' => ['type' => 'float'],
                            'status' => ['type' => 'integer'],
                            'image_url' => ['type' => 'string'],
                            'delivery_time' => ['type' => 'float'],
                            'created_at' => ['type' => 'date', 'format' => 'yyyy-MM-dd HH:mm:ss'],
                            'updated_at' => ['type' => 'date', 'format' => 'yyyy-MM-dd HH:mm:ss']
                            ]
                    ],
                    $this->elasticsearch_rest_type = [
                        '_source' => [
                            'enabled' => true
                        ],
                        'properties' => [
                            'id' => ['type' => 'string']
                        ]
                    ]
                        ]
                    ]
        ];

        return $this->elasticsearch_client->indices()->create($params);
```
# Geo_point
```
"mappings": {
    "my_type": {
      "properties": {
        "location": {
          "type": "geo_point"
        }
      }
    }
  }
```

References: 

https://www.elastic.co/guide/en/elasticsearch/guide/current/mapping.html

https://www.elastic.co/guide/en/elasticsearch/reference/5.4/geo-point.html

https://www.elastic.co/guide/en/elasticsearch/guide/current/decay-functions.html

https://www.elastic.co/blog/geo-location-and-search

https://www.elastic.co/guide/en/elasticsearch/reference/5.0/query-dsl-geo-distance-query.html

http://www.tugberkugurlu.com/archive/elasticsearch-array-contains-search-with-terms-filter