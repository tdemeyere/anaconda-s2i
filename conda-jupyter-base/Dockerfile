# inspired by: 
# https://github.com/openshift-s2i/s2i-wildfly/blob/master/11.0/Dockerfile
# https://github.com/sclorg/s2i-base-container/blob/master/core/Dockerfile

FROM centos/s2i-base-centos7

EXPOSE 8888

ENV ANACONDA_URI=https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    ANACONDA_HOME=/opt/anaconda3

USER root

RUN INSTALL_PKGS="bzip2" && \
    yum update -y && \
    yum install $INSTALL_PKGS -y && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

RUN mkdir $ANACONDA_HOME && \
    chmod a+rw /etc/passwd && \
    chown -R 1001:0 $ANACONDA_HOME && \
    chmod -R 1775 $ANACONDA_HOME && \
    chown -R 1001:0 $HOME && \
    chmod -R 1775 $HOME && \
    umask 0002

USER 1001

RUN curl -o installAnacoda.sh $ANACONDA_URI && \
    chmod a+x installAnacoda.sh && \
    ./installAnacoda.sh -u -b -p  $ANACONDA_HOME && \
    rm installAnacoda.sh && \
    export PATH="$ANACONDA_HOME/bin:$PATH" && \
    conda install jupyter -y

COPY ./s2i/bin/ $STI_SCRIPTS_PATH

CMD $STI_SCRIPTS_PATH/run