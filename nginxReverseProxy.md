Question:
We are having a backup management application UI hosted on Nautilus's backup server in Stratos DC. That backup management application code is deployed under Apache on backup server itself and Nginx is running as a reverse proxy on same server. Apache and Nginx ports are 3001 and 8097 respectively. We have iptables firewall installed on this server. Make the appropriate changes to fulfill the requirements mentioned below:

We want to open all incoming connections to Nginx's port and want to block all incoming connections to Apache's port. Also make sure rules are permanent.

Lost the Question!
Ref:
https://linuxize.com/post/how-to-install-iptables-on-centos-7/
https://upcloud.com/community/tutorials/configure-iptables-centos/
https://phoenixnap.com/kb/iptables-tutorial-linux-firewall#:~:text=Chains%3A%20A%20chain%20is%20a,forward%20another%20type%20of%20packet.

https://www.linode.com/docs/web-servers/nginx/use-nginx-reverse-proxy/
