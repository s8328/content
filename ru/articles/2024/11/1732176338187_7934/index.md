---
# -------------------------------------------------------------------------------------------------------------------- #
# GENERAL
# -------------------------------------------------------------------------------------------------------------------- #

title: "MikroTik: Сертификат Let's Encrypt"
description: ''
icon: 'far fa-file-lines'
categories:
  - 'scripts'
  - 'network'
  - 'security'
tags:
  - 'mikrotik'
  - 'routeros'
  - 'acme'
  - 'ssl'
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

date: '2024-11-21T11:05:43+03:00'
publishDate: '2024-11-21T11:05:43+03:00'
lastMod: '2024-11-21T11:05:43+03:00'

# -------------------------------------------------------------------------------------------------------------------- #
# META
# -------------------------------------------------------------------------------------------------------------------- #

type: 'articles'
hash: 'f892bebc3ecd118ae94827eed31649daccb04ff5'
uuid: 'f892bebc-3ecd-518a-a948-27eed31649da'
slug: 'f892bebc-3ecd-518a-a948-27eed31649da'

draft: 0
---

Алгоритм получения сертификата Let's Encrypt и последующего его продления при помощи скрипта.

<!--more-->

{{< alert "important" >}}
MikroTik [научился](https://help.mikrotik.com/docs/spaces/ROS/pages/2555969/Certificates) автоматически продлевать сертификат Let's Encrypt по истечении 80% срока действия.
{{< /alert >}}

## Получение сертификата

- Создать правило в брандмауэре, которое будет разрешать обращение к порту `80` IP-адресов из списка `acme`:

```
/ip firewall filter add action=accept chain=input dst-port=80 protocol=tcp src-address-list=acme comment="[ROS] ACME"
```

- Включить сервис `www`:

```
/ip service enable www
``` 

- Добавить адрес `0.0.0.0/0` в адрес-лист `acme` на время `00:01:10`:

```
/ip firewall address-list add list=acme address=0.0.0.0/0 timeout=00:01:10 comment="[ROS] ACME running..."
```

- Запустить получение сертификата для домена `example.org`:

```
/certificate enable-ssl-certificate dns-name=example.org
```

- Отключить сервис `www`:

```
/ip service disable www
```

## Скрипт

{{< file "ros.acme.rsc" >}}
