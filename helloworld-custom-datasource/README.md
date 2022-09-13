# Example of customize standalone-openshift.xml
This example is tested on EAP7.2.1 and OCP 3.11.
Also works on EAP7.2.9 and OpenShift Local 4.10.9

How to deploy:
```
oc new-app --template=eap72-basic-s2i -p APPLICATION_NAME=helloworld-custom-datasource -p SOURCE_REPOSITORY_URL=https://github.com/kawakamimanabu/jboss-openshift-examples.git -p SOURCE_REPOSITORY_REF=enable-statistics -p CONTEXT_DIR=helloworld-custom-datasource -e JAVA_OPTS_APPEND=-Dwildfly.statistics-enabled=true
```

Then:
```
# curl -k -v https://helloworld-custom-datasource-test.cloudapps.example.com/helloworld-custom-datasource/api/datasource/status
* About to connect() to helloworld-custom-datasource-test.cloudapps.example.com port 443 (#0)
*   Trying 192.168.122.2...
* Connected to helloworld-custom-datasource-test.cloudapps.example.com (192.168.122.2) port 443 (#0)
* Initializing NSS with certpath: sql:/etc/pki/nssdb
* skipping SSL peer certificate verification
* SSL connection using TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
* Server certificate:
* 	subject: CN=*.cloudapps.example.com
* 	start date: May 13 12:23:01 2019 GMT
* 	expire date: May 12 12:23:02 2021 GMT
* 	common name: *.cloudapps.example.com
* 	issuer: CN=openshift-signer@1557749273
> GET /helloworld-custom-datasource/api/datasource/status HTTP/1.1
> User-Agent: curl/7.29.0
> Host: helloworld-custom-datasource-test.cloudapps.example.com
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Length: 0
< Date: Mon, 27 May 2019 02:14:34 GMT
< Set-Cookie: 2fd5bce01deaf92fc94e271fb8ed3561=75941bcac5dbb56693b981c9b17a0706; path=/; HttpOnly; Secure
< Cache-control: private
< 
* Connection #0 to host helloworld-custom-datasource-test.cloudapps.example.com left intact
```
