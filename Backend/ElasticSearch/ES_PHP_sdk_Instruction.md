# Update By Query

For this example, this would update `status` all the menus in this restaurant(distinguished by `restaurant_id`);

`index`, `type`, `body` are the required fields'

```php
public function updateMenusStatus($restaurant_id, $status) {
        $current_node = $this->getCurrentNode();
        $params['index'] = [$this->elasticsearch_index_prefix.$current_node];
        $params['type'] = ['menu'];
        $params['body']= [
            'query' => [
                'match' => [
                    'restaurant_id' => $restaurant_id
                ]
            ],
            'script' => [
                "inline" => "ctx._source.status = " . (int)$status
            ]
        ];
        try {
            $this->elasticsearch_client->updateByQuery($params);
        } catch (\Exception $e) {
            var_dump($e->getMessage());
        }
    }
```

references:

https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docs-update.html

https://www.elastic.co/guide/en/elasticsearch/reference/5.5/docs-update.html