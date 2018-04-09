# Dynamo DB emulator

Run [DynamoDB local](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.html) on Docker!

## Pull

Docker image pulled to [hub.docker.com](https://hub.docker.com/r/petitviolet/dynamodb-local/).

```shell-session
$ docker pull petitviolet/dynamodb-local
```

## Run

```shell-session
// show help
$ docker run --rm -ti petitviolet/dynamodb-local --help

// in memory
$ docker run -tid -p 8000:8000 --name dynamodb petitviolet/dynamodb-local -inMemory

// persist to file
$ docker run -tid -p 8000:8000 -v $PWD:/data --name dynamodb petitviolet/dynamodb-local
```

## Use

```shell-session
$ aws dynamodb create-table --table-name dev.test_table --attribute-definitions AttributeName=id,AttributeType=S --key-schema AttributeName=id,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5 --endpoint-url http://0.0.0.0:8000
$ aws dynamodb list-tables --endpoint-url http://localhost:8000
```

```shell-session
$ aws dynamodb put-item --endpoint-url http://localhost:8000 --table-name dev.test_table --item '{"id": {"S": "12345"}, "msg": {"S": "Hello World!"} }'
```

```shell-session
$ aws dynamodb get-item --table-name dev.test_table --endpoint-url http://localhost:8000 --key '{"id": {"S": "12345"}}'

{
    "Item": {
        "msg": {
            "S": "Hello World!"
        },
        "id": {
            "S": "12345"
        }
    }
}
```

```shell-session
$ aws dynamodb scan --endpoint-url http://localhost:8000 --table-name dev.test_table
{
    "Count": 1,
    "Items": [
        {
            "msg": {
                "S": "Hello World!"
            },
            "id": {
                "S": "12345"
            }
        }
    ],
    "ScannedCount": 1,
    "ConsumedCapacity": null
}
```
