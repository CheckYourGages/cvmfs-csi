FROM centos:7
LABEL description="CernVM-FS CSI Plugin"

RUN yum install -y https://ecsft.cern.ch/dist/cvmfs/cvmfs-release/cvmfs-release-latest.noarch.rpm && \
    yum install -y cvmfs && yum clean all

COPY default.local /etc/cvmfs

COPY csi-cvmfsplugin /csi-cvmfsplugin
RUN chmod +x /csi-cvmfsplugin
ENTRYPOINT ["/csi-cvmfsplugin"]
