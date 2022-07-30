1. Интересно получилось со stackoverflow.com
```
Trying 151.101.1.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 403 Forbidden
Server: Varnish
Retry-After: 0
Content-Type: text/html
Content-Length: 1918
Accept-Ranges: bytes
Date: Sat, 30 Jul 2022 06:02:44 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-fra19133-FRA
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1659160964.452776,VS0,VE1
X-DNS-Prefetch-Control: off
```
Получил 403 - запрещено - ниже есть сообщение о том что нельзя с моего адреса туда ходить. Возможно потому что идем на 80 порт - а весь интернет перешел на 443

С Яндексом получили редирект:
```
telnet yandex.ru 80                                                                            
Trying 77.88.55.50...
Connected to yandex.ru.
Escape character is '^]'.
GET /search HTTP/1.0
HOST: yandex.ru

HTTP/1.1 302 Moved temporarily
Location: https://yandex.ru/search/?lr=213&redircnt=1659161571.1
NEL: {"report_to": "network-errors", "max_age": 86400, "success_fraction": 0.001, "failure_fraction": 0.1}
Report-To: { "group": "network-errors", "max_age": 86400, "endpoints": [ { "url": "https://dr.yandex.net/nel"}]}
Set-Cookie: yandexuid=7691648381659161571; path=/; expires=Thu, 31 Dec 2037 20:59:59 GMT; domain=.yandex.ru
Set-Cookie: ys=wprid.1659161571633452-10927679172069164838-sas3-0899-b7e-sas-l7-balancer-8080-BAL-8083; path=/; domain=.yandex.ru
Set-Cookie: is_gdpr=0; Path=/; Domain=.yandex.ru; Expires=Mon, 29 Jul 2024 06:12:51 GMT
Set-Cookie: is_gdpr_b=CLryEBChgQE=; Path=/; Domain=.yandex.ru; Expires=Mon, 29 Jul 2024 06:12:51 GMT
Set-Cookie: _yasc=t6HZXyLoqFl2KeZ/hnb+BcUHgRxNjKUI8jiw/DAdDeZRpLsm; domain=.yandex.ru; path=/; expires=Mon, 29-Aug-2022 06:12:51 GMT; secure
X-Content-Type-Options: nosniff
X-Yandex-Items-Count: 15
X-Yandex-Req-Id: 1659161571633452-10927679172069164838-sas3-0899-b7e-sas-l7-balancer-8080-BAL-8083

Connection closed by foreign host.
```
2.![Исключительно ответы 200](https://i.imgur.com/kpw9PGN.png "Исключительно ответы 200")
Долше всего отбрабатывался скрипт от Google(4я строчка) - 618 ms
3. 
```
    dig +short myip.opendns.com @resolver1.opendns.com                                                                  
79.139.215.17
```
4. AS25513
```
 whois -h whois.radb.net 79.139.215.17                                                                                                        
route:          79.139.128.0/17
descr:          Moscow Local Telephone Network (OAO MGTS)
descr:          Moscow, Russia
origin:         AS25513
mnt-by:         MGTS-USPD-MNT
created:        2007-11-01T11:08:49Z
last-modified:  2007-11-01T11:08:49Z
source:         RIPE
remarks:        ****************************
remarks:        * THIS OBJECT IS MODIFIED
remarks:        * Please note that all data that is generally regarded as personal
remarks:        * data has been removed from this object.
remarks:        * To view the original object, please query the RIPE Database at:
remarks:        * http://www.ripe.net/whois
remarks:        ****************************
```
5. Закрыто больше половины:
```
traceroute -An 8.8.8.8                                                                                                                         
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  192.168.137.1 [*]  7.053 ms  7.021 ms  7.004 ms
 2  100.83.0.1 [*]  13.179 ms  13.163 ms  13.153 ms
 3  212.188.1.6 [AS8359]  13.082 ms  13.085 ms  13.072 ms
 4  * * *
 5  72.14.223.74 [AS15169]  13.019 ms 72.14.223.72 [AS15169]  13.005 ms  12.989 ms
 6  108.170.250.99 [AS15169]  12.967 ms 108.170.250.130 [AS15169]  8.404 ms *
 7  142.251.237.154 [AS15169]  116.269 ms 172.253.66.116 [AS15169]  102.208 ms 142.251.238.82 [AS15169]  102.187 ms
 8  172.253.65.82 [AS15169]  102.152 ms 72.14.238.168 [AS15169]  102.136 ms 142.251.238.70 [AS15169]  102.131 ms
 9  172.253.51.243 [AS15169]  102.079 ms 142.250.233.27 [AS15169]  102.093 ms 172.253.51.247 [AS15169]  102.087 ms
10  * * *
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  8.8.8.8 [AS15169]  115.629 ms  115.651 ms  115.611 ms
```
6.![Как у меня все плохо с провайдером и его маршрутизацией](https://i.imgur.com/8aPZc3t.png)
7. 
```
dig A @1.1.1.1 dns.google                                                                                                                          

; <<>> DiG 9.16.1-Ubuntu <<>> A @1.1.1.1 dns.google
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8749
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;dns.google.                    IN      A

;; ANSWER SECTION:
dns.google.             818     IN      A       8.8.4.4
dns.google.             818     IN      A       8.8.8.8

;; Query time: 63 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Сб июл 30 09:54:14 MSK 2022
;; MSG SIZE  rcvd: 71


 dig PTR @1.1.1.1 dns.google                                                                                                                      

; <<>> DiG 9.16.1-Ubuntu <<>> PTR @1.1.1.1 dns.google
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 42077
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;dns.google.                    IN      PTR

;; AUTHORITY SECTION:
dns.google.             300     IN      SOA     ns1.zdns.google. cloud-dns-hostmaster.google.com. 1 21600 3600 259200 300

;; Query time: 91 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Сб июл 30 09:54:36 MSK 2022
;; MSG SIZE  rcvd: 115
```







