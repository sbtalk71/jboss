Shantanu Banerjee : sbtalk@gmail.com

CHANGE LOG
28-04-2018: The JBoss AS/JBoss EAP Lab Manual is prepared and uploaded


To Do:
JBoss CLI Scripts needed to be uploaded.

CLI Script for SSL Configuration

/core-service=management/security-realm=SSLRealm:add

/core-service=management/security-realm=SSLRealm/server-identity=ssl:add(keystore-path="server.keystore", keystore-relative-to="jboss.server.config.dir", keystore-password="secret")

/subsystem=undertow/server=default-server/https-listener=https:write-attribute(name=security-realm,value=SSLRealm)


<security-domain name="mydomain" cache-type="default">
<authentication>
<login-module code="UsersRoles" flag="required">
<module-option name="usersProperties" value="${jboss.server.config.dir}/myusers.properties"/>
<module-option name="rolesProperties" value="${jboss.server.config.dir}/myroles.properties"/>
</login-module>
</authentication>
</security-domain>


Note In order to get working with this configuration, you first have to create the required tables and insert some sample data in it:
create table users(username varchar(32) primary key,password varchar(32));
create table roles(username varchar(32),role varchar(20));
insert into users(username,password) values('scott','scott123');
insert into users(username,password) values('pavan','pavan123');
insert into users(username,password) values('shantanu','shan123');
insert into roles(username,role) values('scott','manager');
insert into roles(username,role) values('pavan','user');
insert into roles(username,role) values('shantanu','manager');


Database Server Login Module:

<security-domain name="mydbdomain" cache-type="default">
<authentication>
<login-module code="Database" flag="required">
<module-option name="dsJndiName" value="<DataSource JNDI Name>"/>
<module-option name="principalsQuery"
value="select password from users where username=?"/>
<module-option name="rolesQuery"
value="select role, 'Roles' from roles where username=?"/>
</login-module>
</authentication>
</security-domain>

