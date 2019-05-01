# systemctl vs chkconfig

Take `httpd` as example:

| Task                          | chkconfig                    | systemctl                           |
| ----------------------------- | ---------------------------- | ----------------------------------- |
| Enable a service              | chkconfig –level 3 httpd on  | systemctl enable httpd.service      |
| Disable a service             | chkconfig –level 3 httpd off | systemctl disable httpd.service     |
| Check the status of a service | service httpd status         | systemctl status httpd.service      |
| List services                 | chkconfig –list              | systemctl list-units –-type=service |
| Start a service               | service httpd start          | systemctl start httpd.service       |
| Stop a service                | service httpd stop           | systemctl stop httpd.service        |
| Restart a service             | service httpd restart        | systemctl restart httpd.service     |
