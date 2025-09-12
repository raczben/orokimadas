This is only for testing/demo purposes.
Our keystore and jetty entry password is the same: Rf7856op

### 1. Generate key:

#### From command line:
Run the following command from the release folder (the build output directory, where the adoration*.jar is placed)

Generate initial keystore (keytool):

```keytool -genkey -alias server-alias -keyalg RSA -keypass Rf7856op -storepass Rf7856op -keystore adorApp.jks```

#### Or use KeyStore Explorer

Download from here: https://keystore-explorer.org/downloads.html

 - File -> New
 - Select `JKS`
 - Generate Key Pair

And place the new `jks` key into release folder.

### 2. Set HTTPS:

Set property `isHttpsInUse=true` in `xxx.conf.properties`

### Note

+1. In case you are using local App server, you may instruct Chrome to accept insecure localhost calls:
`chrome://flags/#allow-insecure-localhost`

+2: In case a certificate renewal happens
- update apache settings to point to new cer and bundle_ca files
- update web app jks -> need to import key pair PKCS#8 - private key + p7b (PKCS#7) files together.

