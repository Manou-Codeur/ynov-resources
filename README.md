# ynov-resources
This uses a google cloud vm instance on a Debian distro
School project to setup different containers which are:
frontend, backend-feed, backend-user & reverseproxy
### Members
- Yanis OUERDANE
- Salim AYACHE
- Abdelghani LARABI

# 1st step - Understanding the project instructions & Environment variables
We had to read all the Project-intrsuctions folder & understand whats needed to be done and execute.
We also had to set the environment variables by using updating the file `set_env.sh` and use the `source set_env.sh`

# 2nd step - Dockerfiles
We had to create different Dockerfiles for backend feed, backend user & reverse proxy

# 3rd step - Compose.yaml
We had to create the compose.yaml file and orchestrate the whole backend, frontend, reverse proxy and database.

### Registry
We had to setup the local registry using this command: `docker run -d -p 5000:5000 --restart always --name registry registry:2`
We also had to pull the `pasciano007/udagram-frontend` and tag it for the local registry with the `docker tag pasciano007/udagram-frontend:latest localhost:5000/udagram-frontend` and push it to the local registry using the `docker push localhost:5000/udagram-frontend`

Once all is done we use the `docker compose up -d` to create the images and run them.

<img width="959" alt="Capture d'écran 2023-10-27 161246" src="https://github.com/Manou-Codeur/ynov-resources/assets/53016507/ae27cd0f-d1e1-474f-82b3-ac506a0aa21b">

# 4th step - Registry
<img width="960" alt="Capture d'écran 2023-10-27 165446" src="https://github.com/Manou-Codeur/ynov-resources/assets/53016507/fd9d1ded-dc82-48af-baf3-de3d85a3d8fc">
<img width="960" alt="Capture d'écran 2023-10-27 173224" src="https://github.com/Manou-Codeur/ynov-resources/assets/53016507/0d569637-0a31-4eef-993c-f254e2ae8dd7">
<img width="785" alt="Capture d'écran 2023-10-27 173535" src="https://github.com/Manou-Codeur/ynov-resources/assets/53016507/4d0acc15-903b-4fff-96a3-c9e88efe4253">

Once all that is done we setup the frontend registry by using the image `konradkleine/docker-registry-frontend`
We create a network using `docker network create reg-net`
We connect to network to the registry using `docker network connect reg-net registry`
To do so, we just had to run this command: `sudo docker run -d -e ENV_DOCKER_REGISTRY_HOST=registry -e ENV_DOCKER_REGISTRY_PORT=5000 --network reg-net -p 1212:80 konradkleine/docker-registry-frontend:v2`

<img width="959" alt="Capture d'écran 2023-10-27 175229" src="https://github.com/Manou-Codeur/ynov-resources/assets/53016507/6aeef748-0345-482b-ad4e-f5024720f782">

