# openssl

[What are OIDs in the context of this keytool command?](https://security.stackexchange.com/questions/133323/what-are-oids-in-the-context-of-this-keytool-command)

## get random value of 16 bit using openssl
```bash
openssl rand -hex 16
```

## get digest value used in bosch.cms
```bash
openssl dgst -sha256 -hex -r /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/stick/cherym31t_navi/stick/bosch.xml | cut -d ' ' -f1
```

## sign certificates using crt and key:
```bash
openssl cms -sign -in /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/stick/cherym31t_navi/cms_tmp/Bosch.msg -out /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/stick/cherym31t_navi/cms_out/Bosch.cms -md sha256 -signer /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/container/security/tooling/swu_code.crt -inkey /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/container/security/tooling/swu_code.priv.key  
```

##  Verifying that a Private Key Matches a Certificate
```bash
openssl x509 -noout -modulus -in /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/container/security/tooling/swu_code.crt |openssl md5
openssl rsa -noout -modulus -in /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/container/security/tooling/swu_code.priv.key |openssl md5
```

## generate pub key using command:
```bash
openssl x509 -pubkey -noout -in /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/container/security/tooling/swu_code.crt
```

##  get serial no, version etc from a certificate
```bash
openssl x509 -in /home/skd7kor/samba/views/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws_GEN/ai_projects/generated/ai_sw_update/container/security/tooling/swu_code.crt  -text -noout
```

## read pvt key from .pem
```bash
openssl rsa -outform pem -in /home/skd7kor/samba/skd7kor_SZH_AI_PRJ_M31T_HIGH_LINUX_16.0F11.vws/ai_sw_update/common/media_tooling/certificates/bosch/private_codekey.pem
``` 

## SRK
```bash
secure-boot-tooling -t --config /usr/share/secure-boot-tooling/conf/signature/sig_PSA-Dev_local.conf --out /tmp/ -v
cat /usr/share/secure-boot-tooling/conf/signature/sig_PSA-Dev_local.conf
xxd -ps -c 32 /tmp/SRK_fuses.bin
```

## convert pem to der
```bash
sudo openssl x509 -in CA/root.crt -inform PEM -out KT/root.der.crt -outform DER
read der: openssl x509 -in KT/root.der.crt  -inform DER -text -noout
read pem: openssl x509 -in  CA/root.crt  -text -noout
```

## Verify if cms is signed using key
```bash
openssl cms -verify -md sha256 -in KT/shwetha_Modified.cms -CAfile CA/root.crt
openssl cms -verify -md sha256 -in KT/shwetha.cms -CAfile CA/root.crt
openssl smime -verify KT/shwetha.cms -CApath CA -CAfile CA/root.crt
```

## how to sign
```bash
sudo openssl cms -sign -in KT/shwetha.txt -out KT/shwetha.cms -md sha256 -signer Bosch/dev_code.crt -inkey Bosch/dev_code_pvt.key
```

## how to decrypt
```bash
sudo openssl enc -aes-128-cbc -d -base64 -iv "1234567890123456" -K "12345678901234567890123456789012" -in shwetha_encrypt.txt -out shwetha_decyypt.txt -p
```

## how to encrypt
```bash
sudo openssl enc -aes-128-cbc -e -base64 -iv "1234567890123456" -K "12345678901234567890123456789012" -in shwetha.txt -out shwetha_encrypt.txt -p
openssl enc -aes-128-cbc -e -base64 -iv "1234567890123456" -K "12345678901234567890123456789012" -in shwetha.txt -out shwetha_encrypt.txt -p
```

## encryption:
```bash
openssl rsautl -oaep -encrypt -inkey /home/skd7kor/samba/skd7kor_AI_PRJ_PSA_RCC_LINUX_16.0T013.vws/ai_sw_update/common/media_tooling/certificates/bosch/swu_code.pub.key -pubin -in /home/skd7kor/samba/views/skd7kor_AI_PRJ_PSA_RCC_LINUX_16.0T013.vws_GEN/ai_projects/generated/ai_sw_update/stick/psarcc/Secure_Boot_Dev/tmp_encrypt_stick/license.xml  | openssl base64 -out /home/skd7kor/samba/license.xml.key
```

# References

https://www.digitalocean.com/community/tutorials/openssl-essentials-working-with-ssl-certificates-private-keys-and-csrs
https://smartnets.wordpress.com/2017/04/27/create-certificate-chain-and-sign-certificates-using-openssl/
https://support.ssl.com/Knowledgebase/Article/View/19/0/der-vs-crt-vs-cer-vs-pem-certificates-and-how-to-convert-them
http://www.gtopia.org/blog/2010/02/der-vs-crt-vs-cer-vs-pem-certificates/
https://stackoverflow.com/questions/49390332/openssl-cms-verify-doesnt-work-with-external-certificate

# Hashtags

#linux #security #openssl