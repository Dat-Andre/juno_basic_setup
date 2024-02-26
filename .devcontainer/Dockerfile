FROM  ubuntu:latest

RUN apt-get update

#Install necessary tools
WORKDIR /
RUN apt-get install --yes wget 
RUN apt-get install --yes curl
RUN apt-get install make
RUN apt-get install --yes build-essential
RUN apt-get install gcc 
RUN apt-get install --yes git
RUN apt-get install --yes jq

# Install Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

ENV PATH="/root/.cargo/bin:${PATH}"

# Update the local crate index
RUN ~/.cargo/bin/cargo search

RUN rustup target add wasm32-unknown-unknown

# Install Go
RUN wget https://golang.org/dl/go1.21.0.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go1.21.0.linux-amd64.tar.gz

ENV GOROOT=/usr/local/go
ENV GOPATH=$HOME/go
ENV GO111MODULE=on
ENV PATH=$PATH:/usr/local/go/bin:$HOME/go/bin

# Install junod
RUN git clone https://github.com/CosmosContracts/juno
WORKDIR /juno
RUN git fetch
RUN git checkout v20.0.0

RUN make install

RUN junod config chain-id juno-1

RUN junod config node https://rpc-juno.itastakers.com:443








