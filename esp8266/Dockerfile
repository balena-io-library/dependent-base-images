# A small glibc/apt base image designed for use in containers
FROM bitnami/minideb

# Install dependencies
RUN apt-get update && apt-get install -yq --no-install-recommends \
    python \
    python-pip \
    python-setuptools && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

# Install tools
RUN pip install -U platformio

# Set the working directory
WORKDIR /usr/src/app

# Set up for building
RUN mkdir -p /assets

# Entry point
CMD ["echo","'No CMD command was set in Dockerfile! Details about CMD command could be found in Dockerfile Guide section in our Docs. Here's the link: http://docs.resin.io/deployment/dockerfile"]
