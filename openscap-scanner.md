# Openscap scanner 

## Walkthrough (Centos 8)

```
dnf install -y openscap-scanner scap-security-guide 
ls -l /usr/share/xml/scap/ssg/content/ssg-centos8-ds.xml
oscap info /usr/share/xml/scap/ssg/content/ssg-centos8-ds.xml

# seems not to download external resource from redhat 
oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_pci-dss --results-arf arf.xml --report report.html /usr/share/xml/scap/ssg/content/ssg-centos8-ds.xml  

# same but downloading it 
oscap xccdf eval --fetch-remote-resources  --profile xccdf_org.ssgproject.content_profile_pci-dss --results-arf arf.xml --report report.html /usr/share/xml/scap/ssg/content/ssg-centos8-ds.xml 

```

## Alternative: done per ssh 

```
https://www.systutorials.com/docs/linux/man/8-oscap-ssh/

```

## Scale OpenSCAP with Redhat Satellite (x machines) 

```
OpenSCAP, Red Hat Satellite, Red Hat Ansible Automation, and Red Hat CloudForms®

```


## Reference / Documentation 

  * https://github.com/RedHatDemos/SecurityDemos/blob/master/2019Labs/RHELSecurityLab/documentation/lab1_OpenSCAP.adoc
  * https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sect-using_oscap

