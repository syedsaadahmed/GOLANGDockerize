FROM golang:1.14

USER root
RUN apt-get update && apt-get install -y sudo
RUN echo "hello ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN apt-get install -y openssh-server htop
RUN mkdir /var/run/sshd

RUN useradd --uid 22222 --user-group --create-home --shell /bin/bash hello

RUN echo 'hello:hello' | chpasswd
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

COPY Files/docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

ENV GOPATH /opt/go:$GOPATH
ENV PATH /opt/go/bin:$PATH
ENV PROJECT learningpack

RUN echo "export GOPATH=/opt/go:$GOPATH" >> /home/hello/.bashrc
RUN echo "export PATH=/opt/go/bin:$PATH" >> /home/hello/.bashrc

#RUN chown -R hello:hello /opt/go

ADD ./source /opt/go/src/${PROJECT}
WORKDIR /opt/go/src/${PROJECT}

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]