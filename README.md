# ITI Docker Lab 2

This repository contains the solution for Docker Lab 2, divided into two main parts: containerizing a legacy Python Flask application and configuring an Nginx web server with custom networking and volumes.

## PART 1: Python Flask Image

### 1. Repository Setup
Cloning the required repository and navigating into the directory:

![Git Clone](Screenshot%202026-03-29%20171131.png)

### 2. Dockerfile Configuration
Creating the Dockerfile:

![Create Dockerfile](Screenshot%202026-03-29%20171150.png)

To handle legacy dependencies in the provided `requirements.txt`, the image is built using `ubuntu:20.04` natively supporting Python 3.8. Here is the configuration used:

![Dockerfile Content](Screenshot%202026-03-29%20192944.png)

### 3. Build the Image
Building the image and tagging it as `iti-flask-lab2`:

![Build Image](Screenshot%202026-03-29%20193057.png)

### 4. Run the Flask Container
Running the container in detached mode, limiting memory to 100MB, and publishing internal port 5000 to localhost port 80:

![Run Container](Screenshot%202026-03-29%20193112.png)

### 5. Push to Docker Hub
Authenticating, correctly tagging the image with the Docker Hub username, and pushing the completed image to the registry:

![Login and Tag](Screenshot%202026-03-29%20194138.png)

![Login and Tag](Screenshot%202026-03-29%20210444.png)

![Push to Hub](Screenshot%202026-03-29%20194204.png)

---

## PART 2: Custom Network, Volumes, and Nginx

### 1. Create the Custom Network
Creating a custom bridge network named `iti-network` with the `10.0.0.0/8` subnet:

![Create Network](Screenshot%202026-03-29%20194653.png)

### 2. Configure the Volume and Index Page
Creating a local directory to serve as a volume, generating the custom `index.html` file, and moving it to the correct parent directory so the volume mounts correctly:

![Create Volume](Screenshot%202026-03-29%20203648.png)

### 3. Custom Nginx Configuration, Execution, and Verification
*(A custom `my-default.conf` file was created in the working directory to overwrite the default Nginx configuration and force it to listen on internal port 8080).*

Deploying the `nginx:alpine` container with the custom network, port mappings (`8080:8080`), and volume mounts. Finally, verifying the setup by successfully curling localhost on port 8080:

![Run Nginx and Verify](Screenshot%202026-03-29%20204208.png)
