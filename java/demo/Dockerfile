FROM open-liberty:kernel

# Add my app and config
COPY --chown=1001:0 target/liberty/wlp/usr/servers/demo/server.xml /config/
COPY --chown=1001:0 target/liberty/wlp/usr/servers/demo/server.env /config/
COPY --chown=1001:0 target/liberty/wlp/usr/servers/demo/bootstrap.properties /config/
COPY --chown=1001:0 target/liberty/wlp/usr/servers/demo/ /opt/ol/helpers/build/configuration_snippets

# Add app to root folder, uses /config/dropins/ for /<project>/index.html
COPY --chown=1001:0 target/demo.war /config/apps/ 

# Optional functionality
ARG MP_MONITORING=true
ARG MP_HEALTH_CHECK=true

EXPOSE 8181
EXPOSE 8543
EXPOSE 9080
EXPOSE 9443

RUN configure.sh