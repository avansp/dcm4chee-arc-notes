# Frequently Raised Problems (FRP)

## DCM4CHEE outputs MySQL complaints on SSL connection

If you've got this output:

> `WARN: Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default if explicit option isn't set. For compliance with existing applications not using SSL the verifyServerCertificate property is set to 'false'. You need either to explicitly disable SSL by setting useSSL=false, or set useSSL=true and provide truststore for server certificate verification.`

it means that your connection to MySQL server uses SSL connection by default but can't verify your certificate.

### Solution

1. Open `$WILDFLY_HOME/standalone/configuration/dcm4chee-arc.xml` file

2. Replace `jdbc:mysql://localhost:3306/pacs` connection-url element with
```
   jdbc:mysql://localhost:3306/pacs?autoReconnect=true&amp;verifyServerCertificate=false&amp;useSSL=true&amp;requireSSL=true
```