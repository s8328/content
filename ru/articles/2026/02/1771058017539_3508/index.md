---
# -------------------------------------------------------------------------------------------------------------------- #
# GENERAL
# -------------------------------------------------------------------------------------------------------------------- #

title: 'MikroTik: SD-карта'
description: ''
icon: 'far fa-file-lines'
categories:
  - 'mikrotik'
tags:
  - 'mikrotik'
  - 'sd'
  - 'disk'
  - 'exfat'
  - 'partition'
  - 'log'
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

date: '2026-02-14T11:33:37+03:00'
publishDate: '2026-02-14T11:33:37+03:00'
lastMod: '2026-02-14T11:33:37+03:00'

# -------------------------------------------------------------------------------------------------------------------- #
# META
# -------------------------------------------------------------------------------------------------------------------- #

type: 'articles'
hash: '4b37dd8ea96f4ba08b2a96da70bb3942fb9047b4'
uuid: '4b37dd8e-a96f-5ba0-bb2a-96da70bb3942'
slug: '4b37dd8e-a96f-5ba0-bb2a-96da70bb3942'

draft: 0
---

Настройка SD-карты для работы с системой логирования.

<!--more-->

## SD-карта

- Создать разделы `swap` (`4096M`), `log` (`16384M`) и `data` (`~`):

```
/disk; add parent=sd1 type=partition partition-size=4096M swap=yes; add parent=sd1 type=partition partition-size=16384M; add parent=sd1 type=partition
```

- Форматировать разделы в файловую систему `ExFAT`:

```
/disk; format sd1-part2 file-system=exfat label=log; format sd1-part3 file-system=exfat label=data
```

## Логирование

- Создать новые события логирования `diskCritical`, `diskError`, `diskInfo` и `diskWarning` для перенаправления логов на SD-карту:

```
/system logging action; set diskCritical disk-file-name=sd1-part2/log.critical; set diskError disk-file-name=sd1-part2/log.error; set diskInfo disk-file-name=sd1-part2/log.info; set diskWarning disk-file-name=sd1-part2/log.warning
```

- Перенаправить топики `critical`, `error`, `info` и `warning` на события логирования `diskCritical`, `diskError`, `diskInfo` и `diskWarning` соответственно:

```
/system logging; set 0 action=diskInfo; set 1 action=diskError; set 2 action=diskWarning; set 3 action=diskCritical
```
