FROM centos:7
MAINTAINER kingson<584281812@qq.com>

# install basic env
RUN yum install -y git && \
    yum install -y curl && \
    yum install -y emacs && \
    yum install -y gcc && \
    yum install -y golang && \
    yum update

# install pip & numpy
RUN yum -y install epel-release
RUN yum -y install python34 && \
    yum -y install python-pip
RUN python -m pip install --upgrade pip
RUN pip install numpy && \
    pip install scipy && \
    pip install matplotlib

ADD https://github.com/ZJU-DistributedAI/ComputingProvider .

WORKDIR /root

# clean local packages
RUN yum clean packages && \
    yum clean headers
CMD ["/bin/echo", "building succeed"]
