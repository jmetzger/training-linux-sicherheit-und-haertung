# Securing Tomcat 

## Run Behind nginx / apache 

## Change Server-Header 

```
/conf/server.xml 
<Connector port="8080" protocol="HTTP/1.1" 
connectionTimeout="20000" 
Server =" "
redirectPort="8443" />


```

## Enable ssl 

```
# In server.xml  under Connector 
SSLEnabled="true" scheme="https" keystoreFile="ssl/keystore.jks" keystorePass="somepass" clientAuth="false" sslProtocol="TLS"
```

## Force ssl 

```
<security-constraint> 
<web-resource-collection> 
<web-resource-name>Protected Context</web-resource-name> 
<url-pattern>/*</url-pattern>
</web-resource-collection> 
<user-data-constraint> 
<transport-guarantee>CONFIDENTIAL</transport-guarantee> 
</user-data-constraint> 
</security-constraint>

```

## Prevent XSS - attacks (Clients side scripts) on cookies 

  * https://owasp.org/www-community/HttpOnly 

## Delete unnecessary apps 

```
[root@main webapps]# ls -lt
drwxr-xr-x 14 tomcat tomcat 4096 Sep 29 15:26 docs
drwxr-xr-x 7 tomcat tomcat 4096 Sep 29 15:26 examples
drwxr-xr-x 5 tomcat tomcat 4096 Sep 29 15:26 host-manager
drwxr-xr-x 5 tomcat tomcat 4096 Sep 29 15:26 manager
drwxr-xr-x 3 tomcat tomcat 4096 Sep 29 15:26 ROOT
```

## Standard-Exception - Seite und Fehlerseiten erden

```
web.xml 
404 /error.jsp 403 /error.jsp 500 /error.jsp
java.lang.Exception /error.jsp

```

## Run with security manager 

```
Start tomcat with open "-security"
This imposes the security manager 

```

## Ref: 

  * https://geekflare.com/de/apache-tomcat-hardening-and-security-guide/
