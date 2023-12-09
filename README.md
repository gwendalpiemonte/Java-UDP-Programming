# Java UDP programming - Practical content questions

## What are the commands to start the unicast emitter and receiver?
```shell
java -jar java-udp-programming-1.0-SNAPSHOT.jar unicast-emitter --delay=0 --frequency=5000 --host=localhost --port=9876
java -jar java-udp-programming-1.0-SNAPSHOT.jar unicast-receiver --port=9876
```

## What are the commands to start the broadcast emitter and receiver?
```shell
java -jar java-udp-programming-1.0-SNAPSHOT.jar broadcast-emitter --delay=5 --frequency=30000 --host=255.255.255.255 --port=9877
java -jar java-udp-programming-1.0-SNAPSHOT.jar broadcast-receiver --port=9877
```

## What are the commands to start the multicast emitter and receiver?
```shell
java -jar java-udp-programming-1.0-SNAPSHOT.jar multicast-emitter --delay=10 --frequency=15000 --host=239.1.1.1 --port=9878 --interface=wlp0s20f3
java -jar java-udp-programming-1.0-SNAPSHOT.jar multicast-receiver --port=9878 --host=239.1.1.1 --interface=wlp0s20f3
```

## What are your conclusions to the following questions?
- What messages do the unicast receiver receives? Why?
- What messages do the broadcast receiver receives? Why?
- What messages do the multicast receiver receives? Why?

## Which command(s) did you use to build the Docker image?
```shell
docker build -t java-udp-programming .
```

## Which command(s) did you use to run the Docker image?
```shell
docker run java-udp-programming
```

## Which command(s) did you use to publish the Docker image?
```shell
export GITHUB_CR_PAT=MY_TOKEN
echo $GITHUB_CR_PAT | docker login ghcr.io -u gwendalpiemonte --password-stdin
docker tag java-udp-programming ghcr.io/gwendalpiemonte/java-udp-programming
docker image rm java-udp-programming
docker push ghcr.io/gwendalpiemonte/java-udp-programming
```

## Which command(s) did you use to run the Docker Compose file?
```shell
docker compose up -d
```
