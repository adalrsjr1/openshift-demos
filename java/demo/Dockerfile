FROM maven

RUN git clone https://github.com/adalrsjr1/openshift-demos.git
RUN mvn -f openshift-demos/java/demo/pom.xml clean package

FROM open-liberty:kernel-java12

COPY --from=0 /openshift-demos/java/demo/target .

# Add my app and config
COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/liberty/wlp/usr/servers/demo/server.xml /config/
COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/liberty/wlp/usr/servers/demo/server.env /config/
COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/liberty/wlp/usr/servers/demo/bootstrap.properties /config/
COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/liberty/wlp/usr/servers/demo/ /opt/ol/helpers/build/configuration_snippets

# Add app to root folder, uses /config/dropins/ for /<project>/index.html
COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/demo.war /config/apps/

# Optional functionality
ARG MP_MONITORING=true
ARG MP_HEALTH_CHECK=true

ENV MAX_KEEP_ALIVE_REQUESTS=-1
ENV MAX_POOL_SIZE=50

# to customize server runing
# ENV JVM_ARGS -Xms0K -Xmx0K

EXPOSE 8181
EXPOSE 8543
EXPOSE 9080
EXPOSE 9443

#CMD ["/opt/ol/wlp/bin/server", "run", "defaultServer"

# RUN configure.sh
