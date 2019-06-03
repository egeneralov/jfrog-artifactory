# license API

- [HA License Information](https://www.jfrog.com/confluence/display/RTF/Artifactory+REST+API#ArtifactoryRESTAPI-HALicenseInformation)
- [Install HA Cluster Licenses](https://www.jfrog.com/confluence/display/RTF/Artifactory+REST+API#ArtifactoryRESTAPI-InstallHAClusterLicenses)
- [Delete HA Cluster License](https://www.jfrog.com/confluence/display/RTF/Artifactory+REST+API#ArtifactoryRESTAPI-DeleteHAClusterLicense)

Try to impliment license handling via

    - name: add user to virtual host
      uri: 
        url: http://0.0.0.0:15672/api/permissions/{{ rabbit_virtualhost }}/{{ rabbit_username }}
        method: PUT
        user: "{{ rabbit_username }}"
        password: "{{ rabbit_password }}"
        return_content: yes
        body: {"configure":".*","write":".*","read":".*"}
        body_format: json
        status_code: 204

ansible eq to

    curl -i -u user:pass -H "content-type:application/json" -XPUT http://0.0.0.0:15672/api/permissions/my_vhost/my_user -d '{"configure":".*","write":".*","read":".*"}'


# systemd unit

    /usr/bin/java \
    -Djava.util.logging.config.file=/opt/jfrog/artifactory/tomcat/conf/logging.properties \
    -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager \
    -Djdk.tls.ephemeralDHKeySize=2048 \
    -Djava.protocol.handler.pkgs=org.apache.catalina.webresources \
    -Dorg.apache.catalina.security.SecurityListener.UMASK=0027 \
    -server \
    -Xms512m \
    -Xmx2g \
    -Xss256k \
    -XX:+UseG1GC \
    -XX:OnOutOfMemoryError="kill -9 %p" \
    -Djruby.compile.invokedynamic=false \
    -Dfile.encoding=UTF8 \
    -Dartdist=deb \
    -Dorg.apache.tomcat.util.buf.UDecoder.ALLOW_ENCODED_SLASH=true \
    -Djava.security.egd=file:/dev/urandom \
    -Djfrog.join.key.paths=/var/opt/jfrog/artifactory \
    -server \
    -Xms512m \
    -Xmx2g \
    -Xss256k \
    -XX:+UseG1GC \
    -XX:OnOutOfMemoryError="kill -9 %p" \
    -Djruby.compile.invokedynamic=false \
    -Dfile.encoding=UTF8 \
    -Dartdist=deb \
    -Dorg.apache.tomcat.util.buf.UDecoder.ALLOW_ENCODED_SLASH=true \
    -Djava.security.egd=file:/dev/urandom \
    -Dartifactory.home=/var/opt/jfrog/artifactory \
    -Dignore.endorsed.dirs= \
    -classpath /opt/jfrog/artifactory/tomcat/bin/bootstrap.jar:/opt/jfrog/artifactory/tomcat/bin/tomcat-juli.jar \
    -Dcatalina.base=/opt/jfrog/artifactory/tomcat \
    -Dcatalina.home=/opt/jfrog/artifactory/tomcat \
    -Djava.io.tmpdir=/opt/jfrog/artifactory/tomcat/temp \
    org.apache.catalina.startup.Bootstrap \
    start

# check log4j

    -Dlog4j.configuration=file:///C:\Dev\log4j.properties

