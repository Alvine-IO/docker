# Docker client library for PHP

This repository provides a client library for docker witten in pure PHP. This library supports the most Features of Docker 1.19 API. 

## Documentation

+ http://doc.alvine.io/alvine.infrastructure.docker/ API
+ https://wiki.schukai.com/display/alvine2/Docker+Komponente

## Install and running alvine-framework

Download Framework from http://download.alvine.io

```bash
wget http://download.alvine.io/alvine.infrastructure.docker-<version>.phar
wget http://download.alvine.io/alvine.infrastructure.docker-<version>.phar.pubkey
````

## Install and running docker-lib

Download Library from http://download.alvine.io

```bash
wget http://download.alvine.io/alvine.framework-<version>.phar
wget http://download.alvine.io/alvine.framework-<version>.phar.pubkey
````

```bash
wget http://download.alvine.io/alvine.framework-1.0.1.phar
wget http://download.alvine.io/alvine.framework-1.0.1.phar.pubkey
````

## Usage

### The client

```php
    $uri = new \Alvine\Net\Resource\URI('http://localhost:4001/');
    $client = new \Alvine\Infrastructure\Docker\Client($uri);
    
    // Optional: connect over proxy
    // $client->setProxy('localhost', 8888);

    $filter = new Alvine\Types\Collection('\Alvine\Infrastructure\Docker\Container\Filter');
    $filter->append(new \Alvine\Infrastructure\Docker\Container\Filter\Status(Alvine\Infrastructure\Docker\Container\Filter\Status::RUNNING));
    $containers = $client->getContainers(true, null, null, null, $filter);
    foreach($containers AS $container) {
        $container = $client->inspectContainer($containers);
        echo $container->getID();
    }
    
    // Run new Container
    $name = 'my';
    $config = new \Alvine\Infrastructure\Docker\Container\Config('debian:jessie');
    $config->setHostname('my')
       ->setDomain('exampe.com')
       ->setCmd('/opt/start.sh');

    $hostConfig = new \Alvine\Infrastructure\Docker\Container\HostConfig();
    $hostConfig->setMemory(5000)
       ->publishAllPorts()
       ->setRestartPolicy(new \Alvine\Infrastructure\Docker\Container\RestartPolicy(\Alvine\Infrastructure\Docker\Container\RestartPolicy::ALWAYS));

    try {
       $client->runContainer($name, $config, $hostConfig);
    } catch(\Exception $ex) {
       echo $ex->getMessage();
    }
    
    // delete a container
    $container = $docker->getContainerByName('my');
    $client->deleteContainer($container->getContainerID());
    
```



