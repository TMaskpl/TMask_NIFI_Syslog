# TMask_NIFI_Syslog



![TMask_NIFI_Syslog](https://user-images.githubusercontent.com/75216446/154860381-4bdcec92-d8aa-49bb-9cbb-e9cee4825890.png)



Tworzymy ListenSyslog - 2514/udp

![SyslogListen](https://user-images.githubusercontent.com/75216446/154860404-ef22c8db-9eb5-421d-99f9-4be5e0a31164.png)


Przekierujmy logi z Mikrotik -> Firewall

Na wejście dostajemy coś takiego np:

firewall,info _influxdb_ forward: in:NAS_BR out:ipip-tunnel1, src-mac 3c:52:82:00:00:00, proto UDP, 10.2.2.236:38267->192.168.0.17:8089, len 1396

Następnie po przepuszczeniu przez ExtractGrok


![GrokExtract](https://user-images.githubusercontent.com/75216446/154860613-b9fc4ca4-c09a-4cee-b0af-fe5ab2589687.png)


otrzymujemy JSON


``
{
  "src_ip" : "10.2.2.236",
  "src_port" : "38267",
  "src_zone" : "BR",
  "proto" : "UDP",
  "LogPrefix" : "firewall,info",
  "dst_port" : "8089",
  "length" : "1403",
  "LogChain" : "_influxdb_ forward",
  "COMMONMAC" : "3c:52:82:00:00:00",
  "dst_zone" : "ipip-tunnel1",
  "dst_ip" : "192.168.0.17"
}
``

Ale nie potrzebujemy tych wszystkich danych wystarczy nam to


![QueryRecord](https://user-images.githubusercontent.com/75216446/154860721-518fcbec-999f-442b-9536-b61d082b8219.png)


plus timestamp_utc

``
{
  "src_ip" : "10.2.2.236",
  "src_port" : "38267",
  "dst_ip" : "192.168.0.17",
  "dst_port" : "8089",
  "timestamp_utc" : 1645385664218
}
``

Następnie ładujemy niezbęde dane do wybranej bazy w celu dalszej analizy

![CheckDB](https://user-images.githubusercontent.com/75216446/154860853-1dbbf533-f368-4154-90e7-64fc44f491ff.png)


