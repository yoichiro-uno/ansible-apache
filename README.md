apache_default_User: "apache"
apache_default_Group: "apache"
apache_default_home: "/usr/share/httpd"
apache_default_GroupID: "48"
apache_default_UserID: "48"
apache_default_listen_port: "80"
apache_default_ServerAdmin: "root@localhost"
apache_default_ServerRoot: "/etc/httpd"
apache_default_BaseDir: "/var/www"
apache_default_DocumentRoot: "/var/www/html"
apache_proxy_conf_dir: "/etc/httpd/conf.d/proxy"
apache_vhosts:
  - apache_vhost_servername: "www.example.com"
    apache_vhost_listen_ip: "*"
    apache_vhost_listen_port: "80"
    apache_vhost_DocumentRoot: "/var/www/html"
    apache_vhost_ErrorLog: "logs/www.example.com_error_log"
    apache_vhost_LogLevel: "warn"
    apache_vhost_LogFormat_combined: '%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"'
    apache_vhost_LogFormat_common: '%h %l %u %t \"%r\" %>s %b'
    apache_vhost_LogFormat_combinedio: '%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\" %I %O'
    apache_vhost_CustomLog: "logs/www.example.com_access_log"
    apache_vhost_CGI_Ailias: "/cgi-bin/"
    apache_vhost_CGI_Path: "/var/www/cgi-bin/"
    apache_vhost_AddDefaultCharset: "UTF-8"
    apache_vhost_proxy:
      - "ProxyPass /examples/websocket/ balancer://tom_ws/ nofailover=Off"
      - "ProxyPassReverse /examples/websocket/ balancer://tom_ws/ nofailover=Off"
      - "ProxyPass /examples/ balancer://tom_ajp/ nofailover=Off"
apache_proxy_balancers:
  - proxy_balancer_name: "tom_ws"
    proxy_members:
      - "ws://172.21.11.142:18009/examples/websocket/ loadfactor=10"
      - "ws://172.21.11.142:18010/examples/websocket/ loadfactor=10" 
  - proxy_balancer_name: "tom_ajp"
    proxy_members:
      - "ajp://172.21.11.142:18009/examples/websocket/ loadfactor=10"
      - "ajp://172.21.11.142:18010/examples/websocket/ loadfactor=10" 
