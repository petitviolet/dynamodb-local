# Dynamo DB emulator

Run [DynamoDB local](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.html) on Docker!

## Run

```shell-session
// show help
$ docker run --rm -ti petitviolet/dynamodb-local --help

// in memory
$ docker run -tid -p 8000:8000 --name dynamodb petitviolet/dynamodb-local -inMemory

// persist to file
$ docker run -tid -p 8000:8000 -v $PWD:/data --name dynamodb petitviolet/dynamodb-local -sharedDb
```

