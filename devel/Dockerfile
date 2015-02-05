FROM perl:5.20
MAINTAINER Siddhartha Basu <siddhartha-basu@northwestern.edu>

COPY *.rpm /rpms/

RUN apt-get update && \
    apt-get -y install alien libaio1 libdb-dev && \
    mkdir -p /rpms && \
    alien -i /rpms/*.rpm && \
    echo '/usr/lib/oracle/11.2/client64/lib' > /etc/ld.so.conf.d/oracle.conf && \
    echo 'export ORACLE_HOME=/usr/lib/oracle/11.2/client64' > /etc/profile.d/oracle.sh

ENV ORACLE_HOME /usr/lib/oracle/11.2/client64/
ENV LD_LIBRARY_PATH /usr/lib/oracle/11.2/client64/lib/
RUN cpanm -n DBD::Oracle git://github.com/dictyBase/Modware-Loader.git@develop DBD::Pg Math::Base36 String::CamelCase

CMD ['modware']
