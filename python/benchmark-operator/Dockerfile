FROM quay.io/centos/centos:stream8

#TODO: Stagify
#RUN dnf install -y https://archive.kernel.org/centos-vault/7.8.2003/virt/x86_64/kubernetes110/kubernetes-client-1.10.3-0.el7.x86_64.rpm
RUN dnf install -y https://rpmfind.net/linux/fedora/linux/development/rawhide/Everything/x86_64/os/Packages/k/kubernetes-client-1.24.4-1.fc38.x86_64.rpm
RUN dnf module -y install python39 && dnf install -y python39 python39-pip && dnf install -y make && dnf install -y git

RUN mkdir /plugin
RUN chmod 777 /plugin
ADD benchmark-operator_plugin.py /plugin
ADD test_benchmark-operator_plugin.py /plugin
ADD requirements.txt /plugin
ADD https://raw.githubusercontent.com/arcalot/arcaflow-plugins/main/LICENSE /plugin
RUN chmod +x /plugin/benchmark-operator_plugin.py /plugin/test_benchmark-operator_plugin.py
WORKDIR /plugin

RUN git clone -b v1.0.1 https://github.com/cloud-bulldozer/benchmark-operator
RUN chmod -R 777 benchmark-operator

RUN pip3 install -r requirements.txt
#RUN /plugin/test_benchmark-operator_plugin.py

USER 1000

ENTRYPOINT ["/plugin/benchmark-operator_plugin.py"]
CMD []

LABEL org.opencontainers.image.source="https://github.com/arcalot/arcaflow-plugins/tree/main/python/benchmark-operator_plugin"
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.vendor="Arcalot project"
LABEL org.opencontainers.image.authors="Arcalot contributors"
LABEL org.opencontainers.image.title="Hello world!"
LABEL io.github.arcalot.arcaflow.plugin.version="1"
