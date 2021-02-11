# Message filter

## Create

```
dotnet new webapi --no-https --name message_receiver

dotnet add package Dapr.AspNetCore --version 1.0.0-rc05

dotnet add package CloudNative.CloudEvents 
dotnet add package CloudNative.CloudEvents.AspNetCore 
dotnet add package Newtonsoft.Json 



dapr run --app-id message-receiver  --components-path /Users/dennis/Desktop/components --app-port 5001 --dapr-http-port 3501 dotnet run

```


## Publish messages

```
dapr publish --pubsub dzpubsub --topic senddata --data '{"id": 2, "name": "Dennis", "message": "Why I Sing the Blues"}'

{"id": 2, "subject": "Dennis", "source": "message-creator", "type": "event",  "message": "Why I Sing the Blues"}
```

## Build

```
REGISTRY_NAME=dzbuild 
az acr login --name $REGISTRY_NAME
az configure --defaults acr=$REGISTRY_NAME
az acr build --registry $REGISTRY_NAME --image message-receiver .
```


## Deploy

```
kubectl apply -f ../../deploy/depl-message-receiver.yaml
```