# 分析

##field分析

```php
$config = new \EasySwoole\ElasticSearch\Config([
    'host'          => '127.0.0.1',
    'port'          => 9200
]);

$elasticsearch = new \EasySwoole\ElasticSearch\ElasticSearch($config);

go(function()use($elasticsearch){
    $bean = new \EasySwoole\ElasticSearch\RequestBean\FieldCaps();
    $bean->setIndex('my-index');
    $bean->setFields('test-field');

    $response = $elasticsearch->client()->fieldCaps($bean)->getBody();
    $response = json_decode($response,true);
    var_dump($response);
})
```

##query分析

```php
$config = new \EasySwoole\ElasticSearch\Config([
    'host'          => '127.0.0.1',
    'port'          => 9200
]);

$elasticsearch = new \EasySwoole\ElasticSearch\ElasticSearch($config);

go(function()use($elasticsearch){
    $bean = new \EasySwoole\ElasticSearch\RequestBean\Explain();
    $bean->setIndex('my-index');
    $bean->setId('my-id');
    $bean->setBody([
        'query' => [
            'bool' => [
                'must' => [
                    ['match' =>
                        [
                            'test-field' => 'abd'
                        ]
                    ]
                ]

            ]
        ]
    ]);
    $response = $elasticsearch->client()->explain($bean)->getBody();
    $response = json_decode($response,true);
    var_dump($response);
})
```