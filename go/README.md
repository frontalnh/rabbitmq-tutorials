# what is rabbitmq?
rabbitmq는 일종의 메세지 브로커이다.
가령 우체국 처럼 받은 메세지를 적합한 수신자에게 전달하는 역할을 한다.

여기서 우체국에 메세지를 보내는 것을 Produce라 하며, 그 주체를 Producer라고 부른다.
메세지를 받는 사람은 메세지를 Consume 한다고 하며, 그 주체를 Consumer라고 부른다.

주로 Produce와 Consumer는 서로 다른 호스트인 경우가 일반적이다.

# Go code for RabbitMQ tutorials

Here you can find Go code examples from [RabbitMQ tutorials](http://www.rabbitmq.com/getstarted.html).

## Requirements

To run this code you need [Go RabbitMQ client](https://github.com/streadway/amqp):

    go get github.com/streadway/amqp


## Code

Code examples are executed via `go run`:

# Hello World

[Tutorial one: "Hello World!"](http://www.rabbitmq.com/tutorial-one-go.html):

    go run send.go
    go run receive.go

단순히 메세지를 주고 받는 튜토리얼

# Work Queues

[Tutorial two: Work Queues](http://www.rabbitmq.com/tutorial-two-go.html):

    go run new_task.go hello world
    go run worker.go

여러 명의 작업자가 큐를 처리하고 균등하게 처리하는 법을 배운다.
또 작업자가 중간에 없어지거나 혹은 큐를 보유하고 있는 서버가 갑자기 없어지는 경우를 처리한다.

# Publish/Subscribe
[Tutorial three: Publish/Subscribe](http://www.rabbitmq.com/tutorial-three-go.html)

    go run receive_logs.go
    go run emit_log.go hello world

위의 tutorial에서는 하나의 consumer에게만 메세지를 보내는 것이 목적이었으며, 때문에 하나의 큐만을 사용했다.
하지만, 이번에는 여러개의 큐를 가진 여러명의 consumer에게 메세지를 보내보도록 하자.

이 경우에는 producer가 보낸 메세지는 모두 exchange로 들어가게 되고, 이 exchange가 exchange type에 따라 적합한 queue로 메세지를 보내어 준다.

# Routing
[Tutorial four: Routing](http://www.rabbitmq.com/tutorial-four-go.html)

    go run receive_logs_direct.go info warn
    go run emit_log_direct.go warn "a warning"

모든 메세지를 받는 것이 아니라 특정한 메세지만 선별적으로 큐에 저장하는 법을 배운다.

# Topics
위의 Routing은 여러개의 기준점을 가지는 것은 어렵다
topic은 특정 규약을 주고 이를 만족하는 메세지는 특정 큐로 보내지도록 규제하는 것이다.


[Tutorial five: Topics](http://www.rabbitmq.com/tutorial-five-go.html)

    go run receive_logs_topic.go "kern.*" "*.critical"
    go run emit_log_topic.go kern.critical "A critical kernel error"

[Tutorial six: RPC](http://www.rabbitmq.com/tutorial-six-go.html)

    go run rpc_server.go
    go run rpc_client.go 10

To learn more, see [Go RabbitMQ client](https://github.com/streadway/amqp).
