FROM centos:7

LABEL Description="This is a build and test environment image for CUBRID"

RUN set -x \
	&& yum -y groupinstall 'Development Tools' \
	&& yum -y install which git cmake systemtap-sdt-devel ncurses-devel java-1.7.0-devel ant elfutils-libelf-devel \
	&& yum clean all

ENV HOME /home
ENV JAVA_HOME /usr/lib/jvm/java

# CUBRID envronment variables
ENV CUBRID $HOME/CUBRID
ENV CUBRID_DATABASES $CUBRID/databases
ENV PATH $CUBRID/bin:$PATH
ENV LD_LIBRARY_PATH $CUBRID/lib
ENV TEST_SUITE medium:sql
ENV BRANCH_TESTTOOLS master
ENV BRANCH_TESTCASES develop

# set timezone for test
ENV TZ Asia/Seoul
RUN ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime
RUN echo 'ZONE="Asia/Seoul' > /etc/sysconfig/clock

VOLUME $HOME

WORKDIR $HOME

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]