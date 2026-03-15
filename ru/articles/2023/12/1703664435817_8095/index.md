---
# -------------------------------------------------------------------------------------------------------------------- #
# GENERAL
# -------------------------------------------------------------------------------------------------------------------- #

title: 'MikroTik: Настройка DoH'
description: ''
icon: 'far fa-file-lines'
categories:
  - 'mikrotik'
tags:
  - 'mikrotik'
  - 'doh'
authors:
  - 'KaiKimera'
sources:
  - ''
license: 'CC-BY-SA-4.0'
complexity: '0'
toc: 1
comments: 1

# -------------------------------------------------------------------------------------------------------------------- #
# DATE
# -------------------------------------------------------------------------------------------------------------------- #

date: '2023-12-27T11:07:16+03:00'
publishDate: '2023-12-27T11:07:16+03:00'
lastMod: '2024-03-31T00:29:00+03:00'

# -------------------------------------------------------------------------------------------------------------------- #
# META
# -------------------------------------------------------------------------------------------------------------------- #

type: 'articles'
hash: 'b6c7c5cd1b0dbfcdedd2f28f87a5064c68b9c659'
uuid: 'b6c7c5cd-1b0d-5fcd-8dd2-f28f87a5064c'
slug: 'b6c7c5cd-1b0d-5fcd-8dd2-f28f87a5064c'

draft: 0
---

Небольшая заметка по настройке DNS over HTTPS ({{< tag "DoH" >}}) на {{< tag "MikroTik" >}}.

<!--more-->

## Установка набора сертификатов

- Скачать пакет сертификатов с сайта `curl.se`:

```text
/tool fetch url="https://curl.se/ca/cacert.pem" dst-path="ros.cacert.pem"
```

- Импортировать сертификаты:

```text
/certificate import file-name="ros.cacert.pem" passphrase="" name="ROS.CA"
```

## Настройка DoH

После установки сертификатов, приступаем к настройке DoH.

### Стандартные DNS

- Стандартные DNS CloudFlare:

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://cloudflare-dns.com/dns-query" verify-doh-cert=yes
```

- Стандартные DNS Google:

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://dns.google/dns-query" verify-doh-cert=yes
```

- Стандартные DNS Quad9:

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://dns10.quad9.net/dns-query" verify-doh-cert=yes
```

- Стандартные DNS OpenDNS:

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://doh.opendns.com/dns-query" verify-doh-cert=yes
```

### DNS с блокировкой вредоносного ПО

- Безопасные DNS CloudFlare:

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://security.cloudflare-dns.com/dns-query" verify-doh-cert=yes
```

- Безопасные DNS Quad9 (Recommended):

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://dns.quad9.net/dns-query" verify-doh-cert=yes
```

- Безопасные DNS Quad9 (Secured):

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://dns9.quad9.net/dns-query" verify-doh-cert=yes
```

- Безопасные DNS Quad9 (Secured w/ ECS support):

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://dns11.quad9.net/dns-query" verify-doh-cert=yes
```

### DNS с блокировкой вредоносного ПО и контента для взрослых

- Семейные DNS CloudFlare:

```text
/ip dns set allow-remote-requests=yes servers=1.1.1.1,8.8.8.8,77.88.8.8 use-doh-server="https://family.cloudflare-dns.com/dns-query" verify-doh-cert=yes
```
