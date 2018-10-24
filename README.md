# Keycloak BCrypt

Add a password hash provider to handle BCrypt passwords inside Keycloak.

## Build
```
mvn clean package
```
Or just get jar built by Travis from the Github Releases page.

## Install
```
curl http://central.maven.org/maven2/org/mindrot/jbcrypt/0.4/jbcrypt-0.4.jar > jbcrypt-0.4.jar
KEYCLOAK_HOME/bin/jboss-cli.sh \
    --command="module add \
        --name=org.mindrot.jbcrypt \
        --resources="jbcrypt-0.4.jar"
cp target/*.jar KEYCLOAK_HOME/standalone/deployments
```
You need to restart Keycloak.

## Use

Set a number of hash iterations (4-30) and bcrypt as an algorithm in a password policy in Keycloak and that's it.
If you don't wand to use the GUI:
```
kcadm.sh  update realms/master -s 'passwordPolicy="hashIterations(10) and hashAlgorithm(bcrypt)"'
```
