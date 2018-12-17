FROM centos:7
MAINTAINER kingson<584281812@qq.com>

# install basic env
RUN yum install -y git && \
    yum install -y curl && \
    yum install -y emacs && \
    yum install -y gcc && \
    yum install -y golang && \
    yum install -y wget 
RUN yum update

# install redis
RUN wget http://download.redis.io/releases/redis-4.0.6.tar.gz
RUN tar -zxvf redis-4.0.6.tar.gz
RUN cd redis-4.0.6 && \
    make MALLOC=libc
RUN cd src && \
    make install
    
WORKDIR /root

ADD https://github.com/ZJU-DistributedAI/MessagingHub/archive/messageing_hub_v0.2 .

# clean local packages
RUN yum clean packages && \
    yum clean headers
CMD ["/bin/echo", "building succeed"]