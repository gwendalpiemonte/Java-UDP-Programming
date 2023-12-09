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

## What are your conclusions to the following questions?
### Unicast Receivers:   
- **Messages Received:** Unicast receivers will only receive messages explicitly directed to them. They won't receive broadcast or multicast messages.
- **Reason:** Unicast messages are targeted and sent to specific receivers by their addresses, ensuring they're the only ones to receive those messages.

### Broadcast Receivers:   
- **Messages Received:** Broadcast receivers will receive messages sent to all devices within the same network.
- **Reason:** Broadcast messages are sent to all devices within the network, hence the receivers on that network receive the broadcasted messages.

### Multicast Receivers:   
- **Messages Received:** Multicast receivers will receive messages sent to a specific multicast group address.
- **Reason:** Multicast messages are sent to a designated group of receivers who have subscribed to that multicast address. Only those receivers get the messages.

### Differences between Docker Compose and Manual Execution:   
- **Message Distribution:** When running with Docker Compose, containers are isolated within networks, ensuring broadcast messages don't interfere with other containers outside the network. In manual execution, without proper network configurations, messages may impact all devices within the same local network, potentially causing unintended interference.
- **Control and Isolation:** Docker Compose allows controlled network isolation, preventing unintended message receptions by unrelated containers. In manual execution, ensuring such isolation and control would require explicit network configurations, which might not be as straightforward or automated as with Docker Compose.

## How and why did the network helped for the broadcast emitters and receivers?
By placing the broadcast emitters and receivers in their own network, Docker confines their messages. 
This means their broadcasts are contained within that network and can't interfere with or be received by other containers outside it.
