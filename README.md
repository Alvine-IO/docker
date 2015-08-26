# Docker client library for PHP

This repository provides a client library for docker for PHP applications.

## Installing and running etcd

Download Library from http://download.alvine.io

```bash
wget http://download.alvine.io/alvine.infrastructure.docker-<version>.phar
wget http://download.alvine.io/alvine.infrastructure.docker-<version>.phar.pubkey
````

## Usage

### The client

```php
    $uri = new \Alvine\Net\Resource\URI('http://localhost:4001/');
    $client = new \Alvine\Infrastructure\Docker\Client($uri);
    
    // Optional: Verbindung über über Proxy
    // $client->setProxy('localhost', 8888);

    $containers = $docker->getContainers();

    $container = $docker->inspectContainer('c27ed447ec06');
    
```
