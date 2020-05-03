FROM golang:1.14


USER root
RUN apt-get update && apt-get install -y sudo
RUN echo "helloworld ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN apt-get install -y openssh-server htop
RUN mkdir /var/run/sshd

RUN useradd --uid 22222 --user-group --create-home --shell /bin/bash helloworld

RUN echo 'helloworld:helloworld' | chpasswd
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

COPY tools/docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]


ENV GOPATH /opt/go:$GOPATH
ENV PATH /opt/go/bin:$PATH
ENV PROJECT learningpack

RUN echo "export GOPATH=/opt/go:$GOPATH" >> /home/helloworld/.bashrc
RUN echo "export PATH=/opt/go/bin:$PATH" >> /home/helloworld/.bashrc

RUN go get -v github.com/derekparker/delve/cmd/dlv
RUN go get -v github.com/mdempsky/gocode
RUN go get -v github.com/uudashr/gopkgs/v2/cmd/gopkgs
RUN go get -v github.com/ramya-rao-a/go-outline
RUN go get -v github.com/stamblerre/gocode
RUN go get -v github.com/rogpeppe/godef
RUN go get -v github.com/sqs/goreturns
RUN go get -v github.com/stamblerre/gocode
RUN go get -v golang.org/x/lint/golint

RUN chown -R helloworld:helloworld /opt/go

ADD ./source /opt/go/src/${PROJECT}
WORKDIR /opt/go/src/${PROJECT}

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]