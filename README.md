Краткое руководство по обходу ЧАСТИ санкций извне для чайников в вебе как я. Показываю на примере того, как я добивался доступа к докам ARM.
1. В cmd/powershell вызываем

`nslookup <имя-сайта> <IP-DNS-сервера>`

Главное, чтобы `<IP-DNS-сервера>` не был заблокирован этим сайтом. В целом можно использовать публичные `1.1.1.1` - DNS от Cloudflare,
`8.8.8.8` - DNS от Google.

Вывод `nslookup developer.arm.com 8.8.8.8` на момент написания:
```
Server:  dns.google
Address:  8.8.8.8

Non-authoritative answer:
Name:    e188909.dsca.akamaiedge.net
Addresses:  2a02:26f0:9500:1c::1749:2c2
          2a02:26f0:9500:1c::1749:2c6
          2.22.31.99
          2.22.31.170
Aliases:  developer.arm.com
          developer.arm.com-v1.edgekey.net
```

2. Из полученных адресов берём любой IPv4 и добавляем в файл `C:\Windows\System32\drivers\etc\hosts` строку

`<IPv4> <имя-сайта>`.

В примере

`2.22.31.99 developer.arm.com`.

3. Заходим на сайт. Проверяем в консоли ошибки, даже если на вид кажется, что всё работает:
<img width="1920" height="1080" alt="Untitled" src="https://github.com/user-attachments/assets/043f81d9-a816-4694-92b9-e168a648442b" />

Ищем ошибки с `net::`. Можно скормить нейронке, чтоб выдала список адресов. Так же смотрим через `nslookup` и добавляем в hosts.

В моём случае было достаточно
```
2.22.31.98 www.arm.com
2.22.31.98 account.arm.com
2.22.31.98 developer.arm.com
2.22.31.98 cdn.designsystem.arm.com
18.165.140.82 learn.arm.com
34.250.165.118 api2.arm.com
40.69.88.149 documentation-service.arm.com
63.140.62.139 smetrics.arm.com
```

4. При переходе на нужные вам страницы сайта так же всё проверяем.
