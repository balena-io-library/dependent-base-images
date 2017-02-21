# A small glibc/apt base image designed for use in containers
FROM bitnami/minideb

# Install dependencies
RUN apt-get update && apt-get install -yq --no-install-recommends \
	binutils-arm-none-eabi \
	ca-certificates \
	cmake \
	curl \
	gcc \
	gcc-arm-none-eabi \
	git \
	libffi-dev \
	libssl-dev \
	libnewlib-arm-none-eabi \
	libstdc++-arm-none-eabi-newlib \
	ninja-build \
	python-dev \
	python-setuptools \
	srecord && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

# Install tools
RUN mkdir -p /temp && cd /temp && \
	curl -k -O https://bootstrap.pypa.io/get-pip.py && python get-pip.py && \
	git clone https://github.com/NordicSemiconductor/pc-nrfutil.git && \
	cd pc-nrfutil && git checkout 0_5_2 && \
	pip install -r requirements.txt && python setup.py install && \
	pip install yotta && \
	cd / && rm -rf /temp

# Copy module.json to the working directory
COPY module.json ./

# Set up for building
RUN yt target bbc-microbit-classic-gcc && yt install && \
	mkdir -p /assets

# Entry point
CMD ["echo","'No CMD command was set in Dockerfile! Details about CMD command could be found in Dockerfile Guide section in our Docs. Here's the link: http://docs.resin.io/deployment/dockerfile"]
