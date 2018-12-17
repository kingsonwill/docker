FROM centos:7
MAINTAINER kingson<584281812@qq.com>

# install basic env
RUN yum install -y git && \
    yum install -y curl && \
    yum install -y emacs && \
    yum install -y gcc && \
    yum install -y golang && \
    yum update

ADD https://github.com/goadesign/goa .
ADD https://github.com/ZJU-DistributedAI/DataClient .

WORKDIR /root

# clean local packages
RUN yum clean packages && \
    yum clean headers
CMD ["/bin/echo", "building succeed"]
