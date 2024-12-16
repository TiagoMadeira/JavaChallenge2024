java version "23.0.1"
Gradle 8.11.1

How to start app:
- gradle build
- docker-compose build
- docker-compose up

Observatios:
- I considered this challenge hard as I didn't had prior experience with springboot, so I was constricted with the time limit.

- The App constains two modules rest and calculator-service which run in two separated docker containers. They comunicate with eachother in a 
request-reply pattern via a kafka broker, which runs in another docker container.

- The Rest module tests are missing! Initially the were implemented with Mckmvc while the App was still running as a whole on localhost, stoped
working once the app was containerized. I figured using KafkaEmbedded could be a good solution and then maybe mock the listener's response but was running out of time and decided to implements the logs.

- Used log4j for the logs but both modules are failing to write the loggs into a file, they are being logged into the console.

- Each HttpResquest is uniquely identified and its Id is returned on the response header.

- Request ids are being propagated via Kafka headers from the publisher to listener but there appears to be an issue with the encoding so they don't match :/.

- The loggs have the following tags to help identifing their source: [Module][kafka/Request(HTTP)][Input/output]
  ex: [calculator-service][Kafka][Input]....

I feel I could have done better with more time... but thats it.

The container running the rest module can be accessed via http://localhost:8080






