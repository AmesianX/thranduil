# Basics
#
FROM mechatoni/trusty-java7
MAINTAINER Toni Mecha <antonio.mecha@siqme.com>

# Install Jira

ENV JIRA_VERSION 6.3.1
RUN curl -Lks http://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-${JIRA_VERSION}.tar.gz -o /root/jira.tar.gz
RUN /usr/sbin/useradd --create-home --home-dir /opt/jira --groups atlassian --shell /bin/bash jira
RUN tar zxf /root/jira.tar.gz --strip=1 -C /opt/jira
RUN chown -R jira:jira /var/atlassian/jira
RUN echo "jira.home = /var/atlassian/jira" > /opt/jira/atlassian-jira/WEB-INF/classes/jira-application.properties
RUN chown -R jira:jira /opt/jira
RUN mv /opt/jira/conf/server.xml /opt/jira/conf/server-backup.xml

ENV CONTEXT_PATH ROOT

ADD launch.bash /launch

# Launching Jira
WORKDIR /opt/jira
VOLUME ["/var/atlassian/jira"]
EXPOSE 8080
USER jira

CMD ["/launch"]
