Example Voting App
=========

Getting started
---------------

Go to [Play with Docker](https://www.play-with-docker.com).
Use the templates (spanner) choose 3 Managers and 2 Workers

Show members of swarm
From any terminal, check the number of nodes in the swarm to identify the manager node that's the Leader:
```
docker node ls

```

or

```
docker node ls | grep Leader

```

On the Leader run these commands:

```
git clone https://github.com/docker/example-voting-app
cd example-voting-app
ls
```

Lets take a look at Services definded in the docker-compose.yml:
```
cat docker-compose.yml
```

To start the Services in this directory run the following command, the -d will run them in detached mode:
```
docker-compose up -d
```

To view the running Containers:
```
docker-compose ps
```

To access Vote use the 5000 link at the top of the screen, and the Results will be at 5001.

At the moment everything is running on the Leader. 

To stop the Services in this directory run the following command:
```
docker-compose down
```

Let's delpoy this now as a Stack on the [Docker Swarm](https://docs.docker.com/engine/swarm/), in this directory run:
```
docker stack deploy --compose-file docker-stack.yml vote
```

To view the running Containers in the Stack:
```
docker stack ps vote
```

To rempove the Stack:
```
docker stack rm vote
```

Architecture
-----

![Architecture diagram](architecture.png)

* A Python webapp which lets you vote between two options
* A Redis queue which collects new votes
* A .NET worker which consumes votes and stores them in…
* A Postgres database backed by a Docker volume
* A Node.js webapp which shows the results of the voting in real time


Note
----

The voting application only accepts one vote per client. It does not register votes if a vote has already been submitted from a client.
