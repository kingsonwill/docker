FROM centos:7
MAINTAINER kingson"584281812@qq.com"

WORKDIR /root
ENV GOROOT /usr/local/go
ENV GOPATH $HOME/go
ENV PATH $GOROOT/bin:$PATH


# install basic env
RUN yum install -y git && \
    yum install -y wget && \
    yum install -y gcc automake autoconf libtool make
RUN yum update 


#install golang
ADD https://studygolang.com/dl/golang/go1.10.3.linux-amd64.tar.gz .
RUN tar -C /usr/local -xzf go1.10.3.linux-amd64.tar.gz && \
    mkdir go


# build geth
RUN cd ~ &&\
    git clone https://github.com/ethereum/go-ethereum 
RUN cd go-ethereum && \
    make geth && \
    cd ~ && \
    mkdir geth && \
    cd geth && \
    mkdir chain


# input geneis
RUN cd geth && \
    touch genesis.json && \
    echo -e "{" > genesis.json && \
    echo -e "\t\"config\": {" >> genesis.json && \
    echo -e "\t\t\"chainId\": 20," >> genesis.json && \
    echo -e "\t\t\"homesteadBlock\": 0," >> genesis.json && \
    echo -e "\t\t\"eip155Block\": 0," >> genesis.json && \
    echo -e "\t\t\"eip158Block\": 0" >> genesis.json && \
    echo -e "\t}," >> genesis.json && \
    echo -e "\t\"alloc\": {" >> genesis.json && \
    echo -e "\t\t\"bc9a3ece02d7cb31cf63dfdfc48db0b82770d014\": {" >> genesis.json && \
    echo -e "\t\t\t\"balance\": \"1000000000000000000000000000000\"" >> genesis.json && \
    echo -e "\t\t}," >> genesis.json && \
    echo -e "\t\t\"457e7d69fd3ac576aa744228e6b3319cde768473\": {" >> genesis.json && \
    echo -e "\t\t\t\"balance\": \"2000000000000000000000000000000\"" >> genesis.json && \
    echo -e "\t\t}," >> genesis.json && \
    echo -e "\t\t\"926ef6011f7c852d30a01c7a4aaa5cbc460588fc\": {" >> genesis.json && \
    echo -e "\t\t\t\"balance\": \"3000000000000000000000000000000\"" >> genesis.json && \
    echo -e "\t\t}" >> genesis.json && \
    echo -e "\t}," >> genesis.json && \
    echo -e "\t\"nonce\": \"0x0000000000000056\"," >> genesis.json && \
    echo -e "\t\"difficulty\": \"0x020000\"," >> genesis.json && \
    echo -e "\t\"mixhash\": \"0x0000000000000000000000000000000000000000000000000000000000000000\"," >> genesis.json && \
    echo -e "\t\"coinbase\": \"0x0000000000000000000000000000000000000000\"," >> genesis.json && \
    echo -e "\t\"timestamp\": \"0x00\"," >> genesis.json && \
    echo -e "\t\"parentHash\": \"0x0000000000000000000000000000000000000000000000000000000000000000\"," >> genesis.json && \
    echo -e "\t\"extraData\": \"0x11bbe8db4e347b4e8c937c1c8370e4b5ed33adb3db69cbdb7a38e1e50b1b82fa\"," >> genesis.json && \
    echo -e "\t\"gasLimit\": \"0xffffffff\"" >> genesis.json && \
    echo -e "}" >> genesis.json


# init & run
RUN cd geth && \
    ~/go-ethereum/build/bin/geth --datadir chain init genesis.json 
RUN cd geth && \
    ~/go-ethereum/build/bin/geth --datadir chain --nodiscover \
                                --rpc --rpcapi "db,web3,eth,net,personal" \
                                --rpccorsdomain "*"  --rpcaddr "0.0.0.0" \
                                --port 16333 --rpcport 8545  console

VOLUME ./geth:~/

EXPOSE 16333 8545

# clean local packages
RUN yum clean packages && \
    yum clean headers
CMD ["/bin/echo", "building succeed"]
