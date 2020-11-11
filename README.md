Shantanu Banerjee : sbtalk@gmail.com

CHANGE LOG
28-04-2018: The JBoss AS/JBoss EAP Lab Manual is prepared and uploaded


To Do:
JBoss CLI Scripts needed to be uploaded.

CLI Script for SSL Configuration

/core-service=management/security-realm=SSLRealm:add

/core-service=management/security-realm=SSLRealm/server-identity=ssl:add(keystore-path="server.keystore", keystore-relative-to="jboss.server.config.dir", keystore-password="secret")

/subsystem=undertow/server=default-server/https-listener=default-https:write-attribute(name=security-realm,value=SSLRealm)

