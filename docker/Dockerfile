FROM centos:7
MAINTAINER kingson<584281812@qq.com>

# install basic env
RUN yum install -y git && \
    yum install -y curl && \
    yum install -y emacs && \
    yum install -y gcc && \
    yum install -y golang && \
    yum update
RUN yum mkdir ~/go && \
    echo "export GOPATH=$HOME/go" >> /etc/profile && \
    source /etc/profile

# build geth
RUN cd ~ &&\
    git clone https://github.com/ethereum/go-ethereum && \
    cd go-ethereum && \
    make geth && \
    cd ~ && \
    mkdir geth && \
    cd geth && \
    mkdir db

# input geneis
RUN touch genesis.json && \
    echo -e "{" > genesis.json && \
    echo -e "\t\"config\": {" >> genesis.json && \
    echo -e "\t\t\"chainId\": 999," >> genesis.json && \
    echo -e "\t\t\"homesteadBlock\": 0," >> genesis.json && \
    echo -e "\t\t\"eip155Block\": 0," >> genesis.json && \
    echo -e "\t\t\"eip158Block\": 0," >> genesis.json && \
    echo -e "\t\t}," >> genesis.json && \
    echo -e "\t\"alloc\": {" >> genesis.json && \
    echo -e "\t\t\"0xeb680f30715f347d4eb5cd03ac5eced297ac5046\": {\"balance\": \"10000000000000000000000000000000\"} " >> genesis.json && \
    echo -e "\t}," >> genesis.json && \
    echo -e "\t\"coinbase\": \"0x0000000000000000000000000000000000000000\"," >> genesis.json && \
    echo -e "\t\"difficulty\": \"0x01\"," >> genesis.json && \
    echo -e "\t\"extraData\": \"0x777573686f756865\"," >> genesis.json && \
    echo -e "\t\"gasLimit\": \"0xffffffff\"," >> genesis.json && \
    echo -e "\t\"nonce\": \"0x0000000000000001\"," >> genesis.json && \
    echo -e "\t\"mixhash\": \"0x0000000000000000000000000000000000000000000000000000000000000000\"," >> genesis.json && \
    echo -e "\t\"parentHash\": \"0x0000000000000000000000000000000000000000000000000000000000000000\"," >> genesis.json && \
    echo -e "\t\"timestamp\": \"0x00\"" >> genesis.json && \
    echo -e "}" >> genesis.json

# init & run
RUN ~/go-ethereum/build/bin/geth --datadir db init genesis.json && \
    ~/go-ethereum/build/bin/geth --datadir "./db" --rpc --rpcaddr=0.0.0.0 \
                                --rpcport 8545 --rpccorsdomain "*" \
                                --rpcapi "eth,net,web3,personal,admin,debug,miner" \
                                --nodiscover --maxpeers 30 --networkid 1981 \
                                --port 30303 --minerthreads 1 console

WORKDIR /root

ADD https://github.com/ZJU-DistributedAI/Dockers .

VOLUME ./geth:~/

EXPOSE 8078 30303

# clean local packages
RUN yum clean packages && \
    yum clean headers
CMD ["/bin/echo", "building succeed"]
