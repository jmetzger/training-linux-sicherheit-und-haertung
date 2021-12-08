# Openscap scanner 

## Walkthrough (Centos 8)

```
dnf install -y openscap-scanner scap-security-guide 
ls -l /usr/share/xml/scap/ssg/content/ssg-centos8-ds.xml
oscap info /usr/share/xml/scap/ssg/content/ssg-centos8-ds.xml

oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_pci-dss --results-arf arf.xml --report report.html /usr/share/xml/scap/ssg/content/ssg-centos8-ds.xml  

```
