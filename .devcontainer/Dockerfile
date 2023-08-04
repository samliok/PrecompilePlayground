# Use a base image that includes both Go and Node.js, such as the official Go image
FROM golang:latest


ENV GOPATH=/go
ENV PATH=$PATH:$GOPATH/bin
ENV AVALANCHEGO_EXEC_PATH=$GOPATH/src/github.com/ava-labs/avalanchego/build/avalanchego
ENV AVALANCHEGO_PLUGIN_PATH=$GOPATH/src/github.com/ava-labs/avalanchego/build/plugins

# Install Node.js and npm using the official Node.js image
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && apt-get install -y nodejs

# # Clone the avalanchego repository
# RUN git clone -b v1.10.4 https://github.com/ava-labs/avalanchego.git $GOPATH/src/github.com/ava-labs/avalanchego

# # Set the working directory to the cloned repository
WORKDIR $GOPATH/src/github.com/ava-labs/

# # Build the avalanchego project using the sh script
RUN curl -LJO https://github.com/ava-labs/avalanchego/releases/download/v1.10.5/avalanchego-linux-amd64-v1.10.5.tar.gz
RUN tar -xzf avalanchego-linux-amd64-v1.10.5.tar.gz
RUN mv avalanchego-v1.10.5 avalanchego
RUN rm avalanchego-linux-amd64-v1.10.5.tar.gz
WORKDIR $GOPATH/src/github.com/ava-labs/avalanchego
RUN mkdir build
RUN mv avalanchego build/avalanchego

RUN  apt-get install --reinstall libc6

RUN curl -sSfL https://raw.githubusercontent.com/ava-labs/avalanche-network-runner/main/scripts/install.sh | sh -s

ENV PATH ~/bin:$PATH
