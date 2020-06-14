Nautilus application development team recently finished beta version of one of their java based application. They are planning to deploy the same on one of the app server in Stratos DC. After having an internal team meeting they have decided to use tomcat application server. Based on the requirements mentioned below complete the task:


a. Install tomcat server on App Server 2 using yum.

b. Configure it to run on port 8086.

c. There is a ROOT.war file on Jump host at location /tmp, deploy the same on this tomcat server and make sure webpage should directly work on base URL i.e without specifying any sub-directory anything like this http://URL/ROOT .

d. You can access the website on LBR link, to do so click on the + button on top of your terminal and select option Select port to view on Host 1 and after adding port 80 click on Display Port.


Sol:

```
sudo yum install tomcat

sftp steve@172.16.238.11
> put ROOT.war

change port in /etc/tomcat/server.xml to 8086

mv ROOT.war /usr/share/tomcat/webapps

systemctl start tomcat 
systemctl enable tomcat
```

Ref:
1. https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-7-on-centos-7-via-yum
2. https://www.baeldung.com/tomcat-deploy-war
