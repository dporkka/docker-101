# How to clone a github repo into docker

## Step 1: Create a Dockerfile

A Dockerfile is a script that contains instructions to build a Docker image. Here's a basic example:

`# Use a base image
FROM ubuntu:latest

# Install necessary packages
RUN apt-get update && apt-get install -y \
    git \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /app

# Clone the GitHub repository
RUN git clone https://github.com/username/repository.git

# Set the working directory to the cloned repository
WORKDIR /app/repository

# Define the command to run when the container starts
CMD ["bash"]`

## Step 2: Build the Docker Image

Navigate to the directory containing the Dockerfile and build the Docker image using the docker build command. Replace my-git-clone with a name for your Docker image.

`docker build -t my-git-clone .`

## Step 3: Run the Docker Container

Once the Docker image is built, you can run a container from this image using the docker run command:

`docker run -it my-git-clone`

This command runs the container in interactive mode and starts a bash session.

## Example Dockerfile Explained

-   **FROM ubuntu**: Uses the latest Ubuntu base image.
-   **RUN apt-get update && apt-get install -y git**: Updates the package list and installs Git.
-   **WORKDIR /app**: Sets the working directory inside the container.
-   **RUN git clone <https://github.com/username/repository.git>**: Clones the specified GitHub repository into the working directory.
-   **WORKDIR /app/repository**: Sets the working directory to the cloned repository.
-   **CMD ["bash"]**: Starts a bash session when the container runs.

## Customizing the Dockerfile

You can customize the Dockerfile according to your needs, such as specifying a particular branch or commit to clone, installing additional dependencies, or running specific commands after cloning the repository.

## Example with Specific Branch

If you want to clone a specific branch, you can modify the `git clone` command in the Dockerfile:

`RUN git clone --branch branch-name https://github.com/username/repository.git`

## Full Example

Here's a complete example Dockerfile for cloning a specific branch and installing additional dependencies:

`FROM ubuntu:latest

RUN apt-get update && apt-get install -y\
    git\
    python3\
    python3-pip\
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN git clone --branch branch-name https://github.com/username/repository.git

WORKDIR /app/repository

RUN pip3 install -r requirements.txt

CMD ["bash"]`

By following these steps, you can clone a GitHub repository into a Docker container, customize the environment, and run any necessary commands.