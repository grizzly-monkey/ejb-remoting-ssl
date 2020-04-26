Enable tls/ssl for remoting port for EAP 

1) Add properties SSL_ENABLED and SSL_STARTTLS like below for remoting-connector 
    
    ```xml<subsystem xmlns="urn:jboss:domain:remoting:1.1">
      <connector name="remoting-connector" socket-binding="remoting" security-realm="ApplicationRealm">
        <properties>
          <property name="SSL_ENABLED" value="true"/>
          <property name="SSL_STARTTLS" value="false"/> set to true if u want STARTTLS and false if TLS ( i recommend using TLS as STARTTLS IS prone to MITM attacks)
        </properties>
      </connector>
    </subsystem>```


2) If you are using default security Realm then just make sure to modify it to use SSL 

```xml<security-realm name="ApplicationRealm">
    <server-identities>
      <ssl>
        <keystore path="server.keystore" relative-to="jboss.server.config.dir" keystore-password="1234567"/>
      </ssl>
    </server-identities>
 </security-realm>```


3) Test your config using  openssl s_client
     ```openssl s_client -connect your_hostname:4447 (for tls)
     openssl s_client -connect your_hostname:4447 -starttls ftp```
