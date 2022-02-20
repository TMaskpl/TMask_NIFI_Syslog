# TMask_NIFI_Syslog



![TMask_NIFI_Syslog](https://user-images.githubusercontent.com/75216446/154860381-4bdcec92-d8aa-49bb-9cbb-e9cee4825890.png)



Tworzymy ListenSyslog - 2514/udp

![SyslogListen](https://user-images.githubusercontent.com/75216446/154860404-ef22c8db-9eb5-421d-99f9-4be5e0a31164.png)


Przekierujmy ligi z Mikrotik -> Firewall

Na wejście dostajemy coś takiego np:

firewall,info _influxdb_ forward: in:NAS_BR out:ipip-tunnel1, src-mac 3c:52:82:00:00:00, proto UDP, 10.2.2.236:38267->192.168.0.17:8089, len 1396

