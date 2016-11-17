
**active tls on frontend**

**on every host**
```
vi /etc/cloudera-scm-agent/config.ini
use_tls=1
```

**generate keystore**
```
$ export JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera; export PATH=$JAVA_HOME/bin:$PATH
$ mkdir /opt/cloudera/security; mkdir /opt/cloudera/security/x509; mkdir /opt/cloudera/security/jks; mkdir /opt/cloudera/security/CAcerts
$ keytool -genkeypair -alias ip-10-0-212-152.us-west-2.compute.internal -keyalg RSA -keystore \
/opt/cloudera/security/jks/cmhost-keystore.jks -keysize 2048 -dname \
"CN=ip-10-0-212-152.us-west-2.compute.internal,OU=Security,O=Example,L=Denver,ST=Colorado,C=US" \
-storepass admin123 -keypass admin123
$ keytool -certreq -alias ip-10-0-212-152.us-west-2.compute.internal \
-keystore /opt/cloudera/security/jks/cmhost-keystore.jks \
-file /opt/cloudera/security/x509/cmhost.csr -storepass admin123 \
-keypass admin123
```

## troubleshooting

```
use cm;
select ATTR,VALUE from CONFIGS WHERE ATTR = 'agent_tls';
update CONFIGS set VALUE = 'false' where ATTR = 'agent_tls';
select * from CONFIGS where ATTR in ('keystore_path','keystore_password','ssl_client_truststore_password');
delete from CONFIGS where ATTR in ('keystore_path','keystore_password','ssl_client_truststore_password');
```
