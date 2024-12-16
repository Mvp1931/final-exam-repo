## This is final exam file for Advance Containers

---

# Statement: Dockerfile: Create a Dockerfile for simple web application

## Task 1: Create a Dockerfile for simple web application

> This is the web application that I will build dockerfile for

![alt text](<Screenshot (20).png>)

> and this is the Dockerfile

```Dockerfile
# base image
FROM php:8.3-cli-bookworm

#working directory
WORKDIR /usr/src/myApp

# copy the files
COPY . /usr/src/myApp

# Expose service port
EXPOSE 9090

# run the command
CMD [ "php","-S","0.0.0.0:9090" ]
```

## Task 2: Build the Docker image.

![alt text](<Screenshot (22).png>)

... some errors in running the command.

lets fix and build again.

![alt text](<Screenshot (24).png>)

> Now the image is built successfully.

### Task 3: Run the Docker Container from image.

![alt text](<Screenshot (31).png>)

...Looks like the container is running.

> Now we can access the application from the browser.

![alt text](<Screenshot (32).png>)
![alt text](<Screenshot (33).png>)

> Application is running successfully on port 9090.

### Improved Dockerfile with Standard practices

```Dockerfile
# Use the official PHP 8.3 image with a specific version
FROM php:8.3.0-cli AS base

# Set the working directory
WORKDIR /usr/src/myapp

# Copy the current directory contents into the container at /usr/src/myapp
COPY . /usr/src/myapp

# Install any needed dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

# Create a non-root user and switch to it
RUN useradd -m appuser
USER appuser

# Expose the port the app runs on
EXPOSE 9090

# Run php -S 0.0.0.0:9090 when the container launches
CMD ["php", "-S", "0.0.0.0:9090"]

```

-   By switching to non root user we improve security of the container.

### Task 4: Push docker image to docker hub.

![alt text](<Screenshot (34).png>)

![alt text](<Screenshot (35).png>)

![alt text](<Screenshot (36).png>)
