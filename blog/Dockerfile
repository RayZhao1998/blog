FROM centos:7

WORKDIR /app
ADD . /app
RUN yum install -y epel-release && \
yum install -y nodejs && npm install hexo-cli -g

EXPOSE 4000


