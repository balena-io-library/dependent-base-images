# A small glibc/apt base image designed for use in containers
FROM bitnami/minideb

# Install dependencies
RUN apt-get update && apt-get install -yq --no-install-recommends \
	binutils-arm-none-eabi \
	ca-certificates \
	make \
	curl \
	gcc-arm-none-eabi \
	git \
	libnewlib-arm-none-eabi \
	python-dev \
	python-setuptools \
	unzip && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

# Install tools
RUN mkdir -p /opt && cd /opt && \
	curl -k -O https://developer.nordicsemi.com/nRF51_SDK/nRF5_SDK_v11.x.x/nRF5_SDK_11.0.0_89a8197.zip && \
	mkdir nRF5_SDK_11.0.0_89a8197 && \
	unzip -q nRF5_SDK_11.0.0_89a8197.zip -d nRF5_SDK_11.0.0_89a8197 && \
	rm nRF5_SDK_11.0.0_89a8197.zip && \
	sed -i 's|/local/gcc-arm-none-eabi-4_9-2015q1||g' nRF5_SDK_11.0.0_89a8197/components/toolchain/gcc/Makefile.posix && \
	mkdir -p /temp && cd /temp && \
	curl -k -O https://bootstrap.pypa.io/get-pip.py && python get-pip.py && \
	git clone https://github.com/NordicSemiconductor/pc-nrfutil.git && \
	cd pc-nrfutil && git checkout 0_5_2 && \
	pip install -r requirements.txt && python setup.py install && \
	cd / && rm -rf /temp

# Set the working directory
WORKDIR /usr/src/app

# Set up for building
RUN mkdir -p /assets

# Entry point
CMD ["echo","'No CMD command was set in Dockerfile! Details about CMD command could be found in Dockerfile Guide section in our Docs. Here's the link: http://docs.resin.io/deployment/dockerfile"]
