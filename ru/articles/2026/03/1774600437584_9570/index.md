---
# -------------------------------------------------------------------------------------------------------------------- #
# GENERAL
# -------------------------------------------------------------------------------------------------------------------- #

title: 'MikroTik: Обновление ROS и загрузчика'
description: ''
icon: 'far fa-file-lines'
categories:
  - 'mikrotik'
tags:
  - 'mikrotik'
  - 'fetch'
  - 'update'
  - 'routeros'
  - 'routerboard'
authors:
  - 'KaiKimera'
sources:
  - 'https://mikrotik.com/download'
  - 'https://help.mikrotik.com/docs/spaces/ROS/pages/328142'
license: 'CC-BY-SA-4.0'
complexity: '0'
toc: 1
comments: 1

# -------------------------------------------------------------------------------------------------------------------- #
# DATE
# -------------------------------------------------------------------------------------------------------------------- #

date: '2026-03-27T11:33:58+03:00'
publishDate: '2026-03-27T11:33:58+03:00'
lastMod: '2026-03-27T11:33:58+03:00'

# -------------------------------------------------------------------------------------------------------------------- #
# META
# -------------------------------------------------------------------------------------------------------------------- #

type: 'articles'
hash: '004f50d4f94d9f117d5aa3efce3619299122eac5'
uuid: '004f50d4-f94d-5f11-8d5a-a3efce361929'
slug: '004f50d4-f94d-5f11-8d5a-a3efce361929'

draft: 0
---

Обновление RouterOS через терминал MikroTik.

<!--more-->

- Скачать версию RouterOS `7.22.1-mmips`:

```
/tool fetch url="https://download.mikrotik.com/routeros/7.22.1/routeros-7.22.1-mmips.npk" dst-path="routeros-7.22.1-mmips.npk"
```

- Перезапустить маршрутизатор для обновления RouterOS:

```
/system reboot
```

- Перезапустить маршрутизатор для обновления загрузчика RouterBoard:

```
/system reboot
```

## Скрипт

- Скачать версию RouterOS `7.22.1-mmips` и перезапустить маршрутизатор:

```
:local ver "7.22.1"; :local arch "mmips"; /tool fetch url="https://download.mikrotik.com/routeros/$ver/routeros-$ver-$arch.npk" dst-path="routeros-$ver-$arch.npk"; :delay 5s; /system reboot
```

- Перезапустить маршрутизатор для обновления загрузчика RouterBoard:

```
/system reboot
```
