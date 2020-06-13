Question:
We are having a backup management application UI hosted on Nautilus's backup server in Stratos DC. That backup management application code is deployed under Apache on backup server itself and Nginx is running as a reverse proxy on same server. Apache and Nginx ports are 6000 and 8092 respectively. We have iptables firewall installed on this server. Make the appropriate changes to fulfill the requirements mentioned below:

We want to open all incoming connections to Nginx's port and want to block all incoming connections to Apache's port. Also make sure rules are permanent.


Sol:
Set Nginx as Reverse proxy to apache. Make below changes in nginx.conf
```
location / {
      proxy_pass http://localhost:3000/;
  }
```

Make changes to iptables:
```
sudo iptables -L
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
sudo iptables -A INPUT -p tcp --dport ssh -j ACCEPT
sudo iptables-save > /etc/sysconfig/iptables
service iptables save

sudo iptables -A INPUT -p tcp --dport 8092 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 6000 -j REJECT
service iptables save
sudo iptables -L
systemctl restart iptables
```

Verify by checking from jump host - 
curl http://172.16.238.16:6000 
curl http://172.16.238.16:8092

Ref:
https://linuxize.com/post/how-to-install-iptables-on-centos-7/
https://upcloud.com/community/tutorials/configure-iptables-centos/
https://phoenixnap.com/kb/iptables-tutorial-linux-firewall#:~:text=Chains%3A%20A%20chain%20is%20a,forward%20another%20type%20of%20packet.

https://www.linode.com/docs/web-servers/nginx/use-nginx-reverse-proxy/
