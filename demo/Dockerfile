FROM jenkins:2.32.3

USER root

# Not available in this distribution from universe (Utopic has 1.6):
RUN wget -q -O /tmp/ngrok.zip https://dl.ngrok.com/ngrok_2.0.19_linux_amd64.zip && \
    cd /usr/local/bin && \
    unzip /tmp/ngrok.zip && \
    rm /tmp/ngrok.zip

COPY plugins /usr/share/jenkins/ref/plugins
RUN chown -R jenkins.jenkins /usr/share/jenkins/ref/plugins

USER jenkins

ADD JENKINS_HOME /usr/share/jenkins/ref

# ngrok management UI on http://localhost:4040/; TODO outside the container just get a connection reset immediately, why?
EXPOSE 4040

CMD ngrok http --log=stdout --log-level=debug 8080 | fgrep ngrok.io & \
    /usr/local/bin/jenkins.sh
