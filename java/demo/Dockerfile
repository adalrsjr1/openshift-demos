# FROM maven
# 
# RUN git clone https://github.com/adalrsjr1/openshift-demos.git
# RUN mvn -f openshift-demos/java/demo/pom.xml clean package
# 
# FROM open-liberty:kernel
# 
# COPY --from=0 /openshift-demos/java/demo/target .
# 
# # Add my app and config
# COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/liberty/wlp/usr/servers/demo/server.xml /config/
# COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/liberty/wlp/usr/servers/demo/server.env /config/
# COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/liberty/wlp/usr/servers/demo/bootstrap.properties /config/
# COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/liberty/wlp/usr/servers/demo/ /opt/ol/helpers/build/configuration_snippets
# 
# # Add app to root folder, uses /config/dropins/ for /<project>/index.html
# COPY --from=0 --chown=1001:0 openshift-demos/java/demo/target/demo.war /config/apps/

FROM open-liberty:kernel

# Optional functionality
ARG MP_MONITORING=true
ARG MP_HEALTH_CHECK=true

EXPOSE 8181
EXPOSE 8543
EXPOSE 9080
EXPOSE 9443

RUN configure.sh
