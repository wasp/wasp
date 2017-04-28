# RabbitMQ Default transport docs
This file points out how the rabbitmq default transport is used.

## Service Discovery
This transport assumes that service discovery is figured out by you using a rabbitmq topic exchange. When registering routes, you
should register every route to your queue. Service names in service discovery can be used to override the exchange. The default exchange
should be used unless explicitely overriden. From a client aspect, publishing a message is as simple as putting it on the exchange.
The service name should not be needed. Exceptions to this can be made for internal services that do not publish routes on the default
exchange.

## Spec
A request message on rabbitmq should look like this:
Note: all parameters are rabbitmq properties, and your information goes in the brackets `{}`. 

```
envelope:
  exchange-name: {name of exchange}
  routing-key: {path with `.` instead of `/` i.e: `foo.1.bar`}
  payload: {message body. If no message body, send `None`}
  properties:
    headers: 
      - **{headers}
      - x-wasp-query-string: {query string}
    reply-to: {name of response queue, this response queue should be unique to the process}
    correlation-id: {correlation_id}
    message-id: {some uuid created for just this message}
    expiration: {time message should stay on the queue before timing out in ms, default could be 30000 (30s)}
    type: {http method (POST,GET,etc.)}
    app-id: {whatever you want}
    content-type: {content-type (i.e. application/json)}
    content-encoding: {content-encoding}
```

and the response should look like:

```
envelope:
  exchange-name: ''  # should be empty, no exchange. This means it goes into rabbits `direct` exchange.
  routing-key: {name of the queue. Should be the requests `reply-to` field}
  payload: {message body. If no message body, send `None`}
  properties:
    headers: 
      - **{headers}
      - Status: {HTTP status code}
    reply-to: {name of response queue, this response queue should be unique to the process}
    correlation-id: {correlation_id, same as the request}
    message-id: {same message id as the request}
    expiration: {time message should stay on the queue before timing out in ms, default could be 30000 (30s)}
    app-id: {whatever you want}
    content-type: {content-type (i.e. application/json)}
    content-encoding: {content-encoding}
```

Youll note that most things map pretty well to rabbitmq. There are a few exceptions where we made up our own rules:
* Type is the http method
* HTTP status is passed as a header
* query string is passed as a header



