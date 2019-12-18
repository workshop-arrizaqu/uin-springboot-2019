# SSL Configuration

[https://geekflare.com/tomcat-ssl-guide/](https://geekflare.com/tomcat-ssl-guide/)

## Example

```
[root@mos-dev ssl]# keytool -genkey -alias mosstaging.dwidayatour -keyalg RSA -keysize 2048 -keystore dwidaya.jks
Enter keystore password:
Re-enter new password:
What is your first and last name?
What is the name of your organizational unit?
  [Unknown]:  tour and travel
What is the name of your organization?
  [Unknown]:  dwidaya tour
What is the name of your City or Locality?
  [Unknown]:  north of jakarta
What is the name of your State or Province?
  [Unknown]:  DKI Jakarta
What is the two-letter country code for this unit?
Is CN=mosstaging.dwidayatour.co.id, OU=tour and travel, O=dwidaya tour, L=north of jakarta, ST=DKI Jakarta, C=62 correct?
Enter key password for <mosstaging.dwidayatour>
        (RETURN if same as keystore password):
Re-enter new password:
[root@mos-dev ssl]# ls
AddTrustExternalCARoot.crt  dwidaya.jks  SectigoRSADomainValidationSecureServerCA.crt  STAR_dwidayatour_co_id.crt  USERTrustRSAAddTrustCA.crt
[root@mos-dev ssl]# keytool -certreq -alias mosstaging.dwidaya -keyalg RSA -file  -keystore bloggerflare.jks
AddTrustExternalCARoot.crt                    SectigoRSADomainValidationSecureServerCA.crt  USERTrustRSAAddTrustCA.crt
dwidaya.jks                                   STAR_dwidayatour_co_id.crt
[root@mos-dev ssl]# keytool -certreq -alias mosstaging.dwidaya -keyalg RSA -file STAR_dwidayatour_co_id.crt -keystore dwidaya.jks
Enter keystore password:
keytool error: java.lang.Exception: Alias <mosstaging.dwidaya> does not exist
[root@mos-dev ssl]# keytool -certreq -alias mosstaging.dwidayatour -keyalg RSA -file STAR_dwidayatour_co_id.crt -keystore dwidaya.jks
Enter keystore password:
[root@mos-dev ssl]# keytool -importcert -alias root -file
AddTrustExternalCARoot.crt                    SectigoRSADomainValidationSecureServerCA.crt  USERTrustRSAAddTrustCA.crt
dwidaya.jks                                   STAR_dwidayatour_co_id.crt
[root@mos-dev ssl]# keytool -importcert -alias root -file AddTrustExternalCARoot.crt -keystore dwidaya.jks
Enter keystore password:
Owner: CN=AddTrust External CA Root, OU=AddTrust External TTP Network, O=AddTrust AB, C=SE
Issuer: CN=AddTrust External CA Root, OU=AddTrust External TTP Network, O=AddTrust AB, C=SE
Serial number: 1
Valid from: Tue May 30 18:48:38 CST 2000 until: Sat May 30 18:48:38 CST 2020
Certificate fingerprints:
         MD5:  1D:35:54:04:85:78:B0:3F:42:42:4D:BF:20:73:0A:3F
         SHA1: 02:FA:F3:E2:91:43:54:68:60:78:57:69:4D:F5:E4:5B:68:85:18:68
         SHA256: 68:7F:A4:51:38:22:78:FF:F0:C8:B1:1F:8D:43:D5:76:67:1C:6E:B2:BC:EA:B4:13:FB:83:D9:65:D0:6D:2F:F2
         Signature algorithm name: SHA1withRSA
         Version: 3

Extensions:

#1: ObjectId: 2.5.29.35 Criticality=false
AuthorityKeyIdentifier [
KeyIdentifier [
0000: AD BD 98 7A 34 B4 26 F7   FA C4 26 54 EF 03 BD E0  ...z4.&...&T....
0010: 24 CB 54 1A                                        $.T.
]
[CN=AddTrust External CA Root, OU=AddTrust External TTP Network, O=AddTrust AB, C=SE]
SerialNumber: [    01]
]

#2: ObjectId: 2.5.29.19 Criticality=true
BasicConstraints:[
  CA:true
  PathLen:2147483647
]

#3: ObjectId: 2.5.29.15 Criticality=false
KeyUsage [
  Key_CertSign
  Crl_Sign
]

#4: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: AD BD 98 7A 34 B4 26 F7   FA C4 26 54 EF 03 BD E0  ...z4.&...&T....
0010: 24 CB 54 1A                                        $.T.
]
]

Trust this certificate? [no]:  yes
Certificate was added to keystore
[root@mos-dev ssl]# keytool -importcert -alias intermediate -file
AddTrustExternalCARoot.crt                    SectigoRSADomainValidationSecureServerCA.crt  USERTrustRSAAddTrustCA.crt
dwidaya.jks                                   STAR_dwidayatour_co_id.crt
[root@mos-dev ssl]# keytool -importcert -alias intermediate -file USERTrustRSAAddTrustCA.crt -keystore dwidaya.jks
Enter keystore password:
Certificate was added to keystore
[root@mos-dev ssl]# keytool -importcert -file SectigoRSADomainValidationSecureServerCA.crt -keystore dwidaya.jks -alias mosstaging.dwidayatour
Enter keystore password:
keytool error: java.lang.Exception: Public keys in reply and keystore don't match
[root@mos-dev ssl]# keytool -importcert -file SectigoRSADomainValidationSecureServerCA.crt -keystore dwidaya.jks -alias mosstaging.dwidaya
Enter keystore password:
Certificate was added to keystore
[root@mos-dev ssl]# keytool -importcert -file  -keystore dwidaya.jks -alias mosstaging.dwidaya
AddTrustExternalCARoot.crt                    SectigoRSADomainValidationSecureServerCA.crt  USERTrustRSAAddTrustCA.crt
dwidaya.jks                                   STAR_dwidayatour_co_id.crt
[root@mos-dev ssl]# keytool -importcert -file STAR_dwidayatour_co_id.crt -keystore dwidaya.jks -alias mosstaging.dwidaya
Enter keystore password:
keytool error: java.lang.Exception: Certificate not imported, alias <mosstaging.dwidaya> already exists
[root@mos-dev ssl]# keytool -importcert -file STAR_dwidayatour_co_id.crt -keystore dwidaya.jks -alias mosstaging.dwidayatour
Enter keystore password:
keytool error: java.security.cert.CertificateParsingException: java.io.IOException: ObjectIdentifier() -- data isn't an object ID (tag = 49)
[root@mos-dev ssl]# chmod 775 /home/dtadmin/ssl/
AddTrustExternalCARoot.crt                    SectigoRSADomainValidationSecureServerCA.crt  USERTrustRSAAddTrustCA.crt
dwidaya.jks                                   STAR_dwidayatour_co_id.crt
[root@mos-dev ssl]# chmod 775 /home/dtadmin/ssl/dwidaya.jks
```



