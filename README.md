# hermes docker-compose running

## how  to run

* start

```code
docker-compose up -d

```

* create group && topic

```code
group:

curl -X POST -H "Content-Type: application/json" http://localhost:8090/groups -d '{"groupName": "dalong"}'

topic:
curl -X POST -H "Content-Type: application/json" http://localhost:8090/topics -d '{
    "name": "dalong.userlogin",
    "description": "This is userlogin topic",
    "contentType": "JSON",
    "retentionTime": {
        "duration": 1
    },
    "owner": {
        "source": "Plaintext",
        "id": "dalong"
    }
}'
```

* create subscriptions

```code
curl -X POST -H "Content-Type: application/json" http://localhost:8090/topics/dalong.userlogin/subscriptions -d '{
    "topicName": "dalong.userlogin",
    "name": "userlogin", 
    "description": "This is my subscription",
    "endpoint": "http://benthos:4195/", 
    "owner": {
        "source": "Plaintext",
        "id": "dalong"
    }
}'
```

* send message

```code
curl -X POST -H "Content-Type: application/json" http://localhost:8080/topics/dalong.userlogin -d '{"message": "Hello world!"}'
```

* view webhook logs

```code
docker-compose logs -f benthos
```