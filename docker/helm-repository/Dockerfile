FROM tor2/centos-source-base:4.0.0
MAINTAINER Kolla Project (https://launchpad.net/kolla)


ENV helm_version 2.1.3
ENV helm_port 8879
ENV helm_address 0.0.0.0









    


RUN yum -y install git jq python-pip && yum clean all

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
    && python get-pip.py \
    && rm get-pip.py

RUN pip install pyyaml

RUN curl -Lo /tmp/helm-v${helm_version}-linux-amd64.tar.gz  http://storage.googleapis.com/kubernetes-helm/helm-v${helm_version}-linux-amd64.tar.gz \
    && sudo tar --strip-components 1 -C /usr/bin linux-amd64/helm -zxvf /tmp/helm-v${helm_version}-linux-amd64.tar.gz \
    && sudo chmod 755 /usr/bin/helm \
    && rm /tmp/helm-v${helm_version}-linux-amd64.tar.gz

RUN useradd --user-group --create-home --home-dir /home/helm helm \
    && sudo mkdir /helm-repo \
    && sudo chmod 755 /helm-repo \
    && sudo chown -R helm: /helm-repo/

USER helm

RUN helm init --client-only

CMD helm serve --address $helm_address:$helm_port --repo-path /helm-repo


