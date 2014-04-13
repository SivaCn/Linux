find process that are listening or running on particular port:

  $ netstat -tulpn
  
  OUTPUT:
    (Not all processes could be identified, non-owned process info
    will not be shown, you would have to be root to see it all.)
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address               Foreign Address             State       PID/Program name   
    tcp        0      0 0.0.0.0:4545                0.0.0.0:*                   LISTEN      7178/python2.6      
    tcp        0      0 0.0.0.0:4546                0.0.0.0:*                   LISTEN      7178/python2.6      
    tcp        0      0 0.0.0.0:4547                0.0.0.0:*                   LISTEN      8537/python2.6      
    tcp        0      0 0.0.0.0:902                 0.0.0.0:*                   LISTEN      -   
    .....
    .....
    .....
  
  process python2.6 is running as PID #8537, to investigate, use
  
  $ ls -l /proc/<PID>/exe


Delete all pyc files in a project:

  find . -name "*.pyc" -exec rm -f {} \;


Find All Machines on the same Network:

  Method I
    #!/bin/bash
    for ip in 192.168.0.{1..254}; do
      ping -c 1 -W 1 $ip | grep "64 bytes" &
    done

  Method II
    arp -a

Get Hostname by IP

  $ host <ip>

Get IP address by Host Name

  $ host <domain name>

