# DoFler v6
DoFler (short for Dashboard Of Fail) is a web-based front-end tying data from a wide variety of different network sniffing and analysis tools. The web UI is intended to be displayed on a projector at Hacking/Information Security conferences, however I have heard of numerous people running DoFler in their own home labs, PwnPads, etc.

## Installation

### Requirements
DoFler only requires `docker` to run.  
To function, it also requires a network interface connected to a span port on your switch (or similar).
The network interface needs to be configured to allow multiple docker containers to access it, you can read more about that [here](http://stevemcgrath.io/2017/07/docker-containers--network-sniffing/).

### Ansible
To make setup easier, we provide an ansible playbook for Ubuntu (16.04).   
In order to use it, run `./bin/ansible <network interface>`.  
Replace `<network interface>` with the network interface connected to your span port.

## Running
To start DoFler, run `./bin/up`.  
After it's started, you can connect to the web interface on `http://localhost:8080`.

## Development
For development we build all the containers locally, this requires you to check out the individual container repositories in the same parent directory as this repository, as such:
```
dofler
docker-web-api
docker-nsfw
```

### Environment
A few scripts are provided for building, starting, stopping and running commands against the development environment:  

`./bin/up-dev` - For starting the environment  
`./bin/down-dev` - For removing the environment  
`./bin/build-dev` - For (re)building the environment  
`./bin/run-dev` - For spinning up a container of the specified service and run a command against it 

To start the dev environment, run `./bin/up-dev`.  
To rebuild the dev environment, run `./bin/build-dev`.  
If you wish to start a single container, run `./bin/up-dev <container>`.  
To create an interactive container, run `./bin/run-dev <container> /bin/sh`.

The development environment will build the containers locally, and hot-reload code when changed.

### Debugging
Most container repositories contain Visual Studio Code configuration for debugging.  
To use it, open the container directory in Visual Studio Code, go to the `Debug` menu and press `Start Debugging`.

### Running the development environment remotely
As the development environment requires a network tap, you might want to run it on a remote machine.
To tell docker compose to use the docker daemon on another host, export the `DOCKER_HOST` environment variable:
```
export DOCKER_HOST=tcp://docker-host:2375
```
Note that this requires the docker daemon to listen on a public interface.

## License
See [LICENSE.md](LICENSE.md)
