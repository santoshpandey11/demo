### Required API output

Calling the API returns:

- The application version.
- The latest git commit SHA.
- A description of the application.

Sending a GET request to http://localhost:8000/version should return similar to the following:

```json
"myapplication": [
  {
    "version": "1.0.0",
    "lastcommitsha": "abc57858585",
    "description" : "pre-interview technical test"
  } ]
```

### Solution Implementation

Calling the API returns:
A minimal API built with Express JS and run with Docker (distroless/nodejs) that exposes a HTTP API server.

Infrastructure
Ubuntu 18.4
Software:
Git, Travis, Vagrant, virtualbox and Ansible
### CI Builds

The Travis CI build is configured in `.travis.yml`

Travis:
- Writes the current git rev SHA (short) to a file that is baked into the image.
- Builds the application-in Docker.
- Runs some basic tests.
- Deploys the docker image to [Docker Hub](https://hub.docker.com/repository/docker/sammcj/anz-test-2/).
- trigger Ansible playbook to provision kubernetes and deploy application

 need to set the `DOCKER_USERNAME` , `DOCKER_PASSWORD` , `KUBERNETESENDPOINT` , `KUBERNETESCERTIFICATE` `KUBERNETESTOKEN` variables in the Travis UI.

### Requirements

To use the provided Makefile the following are required:

- `make`
- `jq`
- `docker`
- `git`

And if you want to run the tests manually you'll need