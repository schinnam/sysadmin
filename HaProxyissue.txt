Troubleshoot and fix the issue, and make sure haproxy service is running on Nautilus LBR server.

Sol:
haproxy -c -V -f /etc/haproxy/haproxy.cfg

Fixed syntax issue and restarted haproxy.
