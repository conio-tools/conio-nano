FROM bde2020/hadoop-base:2.0.0-hadoop3.2.1-java8

MAINTAINER Ivan Ermilov <ivan.s.ermilov@gmail.com>

HEALTHCHECK CMD curl -f http://localhost:8042/ || exit 1

ADD run.sh /run.sh
RUN chmod a+x /run.sh

RUN apt-get update
RUN apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
RUN apt-get update
RUN apt install -y docker-ce-cli

RUN rm $HADOOP_HOME/etc/hadoop/container-executor.cfg
ADD container-executor.cfg $HADOOP_HOME/etc/hadoop/container-executor.cfg

RUN groupadd hadoop
RUN useradd nm -u 2000 -M -G hadoop

RUN useradd conio -u 2001 -M

RUN chown root $HADOOP_HOME/
RUN chown root $HADOOP_HOME/etc/
RUN chown root $HADOOP_HOME/etc/hadoop
RUN chown root $HADOOP_HOME/etc/hadoop/container-executor.cfg
RUN chgrp hadoop $HADOOP_HOME/
RUN chgrp hadoop $HADOOP_HOME/etc/
RUN chgrp hadoop $HADOOP_HOME/etc/hadoop/
RUN chgrp hadoop $HADOOP_HOME/etc/hadoop/container-executor.cfg

RUN chown root $HADOOP_HOME/bin/container-executor
RUN chgrp hadoop $HADOOP_HOME/bin/container-executor
RUN chmod 6050 $HADOOP_HOME/bin/container-executor

EXPOSE 8042

CMD ["/run.sh"]
