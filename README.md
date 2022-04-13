# tutorial-deploy-container-to-cloud
Project made for learning how to deploy docker containers with GCP, following steps mentioned in [How to Deploy Docker Containers to The Cloud](https://towardsdatascience.com/how-to-deploy-docker-containers-to-the-cloud-b4d89b2c6c31).

Check [wsargent Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet) repository out if you want to learn more about Docker.

## You Will Learn How To:

- Install Docker for Windows and WSL2
- Build your first Docker Image 
- Deploy your Docker Image with GCP

## Install Docker for Windows and WSL2
If you are using WSL2 do not install follow the installation instructions for Linux. What is reccommended, far quicker and easier, is installing Docker Desktop for Windows. To install Docker Desktop for Windows follow the steps mentioned in Docker Docs [Install Docker Desktop on Windows](https://docs.docker.com/desktop/windows/install/). Pay attention to **WSL2 Backend** configurations so Docker Desktop also works for WSL2.

## Build Your First Docker Image
To create a Docker image you'll need a Dockerfile. A Dockerfile is a set of instructions that will be sequentially executed by Docker to create a contained file system to run your app. Here is a list of [Dockerfile instructions](https://github.com/wsargent/docker-cheat-sheet#instructions) and what they do and, with some examples.

Once you have you Dockerfile you can build an image following the file instructions and the `docker build` command.

```bash
docker build -t [IMAGE-NAME] .
```
The `-t` flag lets you specify your image name and . tells docker to build an image including all files in current directory.

## Deploy Your Docker Image With GCP

To build deploy your image to GCP you'll need to:

1. [install Cloud SDK](https://cloud.google.com/sdk/docs/install#linux).
2. Authenticate Cloud SDK
```bash
gcloud auth login --no-browser
```

The `--no-browser` lets you authenticate gcloud in a machine without a web browser. Copy the url that will be given to you in a browser from another machine and login.

3. Set your active GCP project
```bash
gcloud set project [PROJECT-ID]
```
4. Configure docker to use your GCP credentials
```bash
gcloud auth configure-docker
```
5. Upload container to GCR (Google Container Register) by submitting it to Cloud Build with `gcloud builds submit`.
```bash
gcloud builds submit --tag eu-gcr.io/[PROJECT-ID]/[IMAGE-NAME]
```
The GCR location is provided to the `--tag` flag.

