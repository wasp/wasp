# wasp

Wasp is a asynchronous "transport-agnostic" web framework project.
The goal is to allow you to spin up a RESTful web service that can listen on any transport
such as HTTP, RabbitMQ, or others.

It is a project designed to make microservices; specifically python, but we hope
this project will grow to other languages as well.

## Language agnostic concepts
The patterns used in wasp are language agnostic. 
You should be able to call other services in different languages
assuming they all follow the same patterns. Wasp frameworks have a pluggable
architecture for the transport layer, which allows you to switch from
http to using a message bus, or vice-versa. You could even listen on both
at the same time without having to modify your code at all.

## Etymology
`wasp` stands for a Wicked Async Services Platform. 
It can also stand for Web Application Service Platform if that suits you better.
Wasps are also a very powerful insect. Most wasps are strong enough to stand up for (as in, defend) themselves.
However, wasps work as a hive, and achieve a single system. In otherwords, they are "microserviced".

Also, the yellow jacket wasp is one of my (nhumrich) greatest fears, so naming this wasp
is also a wierd way of "conquering" my fears.

## Current frameworks
[waspy - Python asyncio framework](https://github.com/wasp/waspy)

## License
Apache-2.0

