Our monitoring tool has reported an issue in Stratos Datacenter where one of our app server has some issue as its Apache service is not reachable on port 6400 (which is our Apache port). Either service it self is down or some firewall or something is causing the issues.


Try to test yourself using tools like telnet and netstat etc and fix the issue once identified. Also make sure Apache is reachable from jump host without compromising any security settings.

Sol:
```
curl http://172.16.238.10:6400 --> no respose

systemctl start httpd --> Error about ServerName

ServerName 172.16.238.10

systemctl start httpd --> Error regarding port

netstat -plant --> sendmail already using port 6400

systemctl kill sendmail

systemctl restart httpd --> successful start

curl http://172.16.238.10:6400 --> No route to host

iptables -L
iptables -S
iptables -L INPUT -nv --> shows config in /etc/sysconfig/iptables

vi /etc/sysconfig/iptables
-A INPUT -m state --state NEW -p tcp --dport 8080 -j ACCEPT --> add above REJECT ALL

iptables-save

systemctl restart iptables


```

Worked!!!

Ref:
- https://www.maketecheasier.com/fix-no-route-to-host-error-linux/
- https://www.maketecheasier.com/secure-linux-desktop-with-iptables/
- https://community.kodekloud.com/t/linux-network-services-apache-not-running-on-app1-port-8081/5891/18
