---
# -------------------------------------------------------------------------------------------------------------------- #
# GENERAL
# -------------------------------------------------------------------------------------------------------------------- #

title: 'MikroTik: Резервная копия конфигурации'
description: ''
icon: 'far fa-file-lines'
categories:
  - 'mikrotik'
tags:
  - 'mikrotik'
  - 'backup'
  - 'restore'
authors:
  - 'KaiKimera'
sources:
  - 'https://help.mikrotik.com/docs/spaces/ROS/pages/40992852/Backup'
license: 'CC-BY-SA-4.0'
complexity: '0'
toc: 1
comments: 1

# -------------------------------------------------------------------------------------------------------------------- #
# DATE
# -------------------------------------------------------------------------------------------------------------------- #

date: '2026-03-16T18:20:10+03:00'
publishDate: '2026-03-16T18:20:10+03:00'
lastMod: '2026-03-16T18:20:10+03:00'

# -------------------------------------------------------------------------------------------------------------------- #
# META
# -------------------------------------------------------------------------------------------------------------------- #

type: 'articles'
hash: 'ed9d9d880fdf616690688d915dcdcebdc9965a1d'
uuid: 'ed9d9d88-0fdf-5166-b068-8d915dcdcebd'
slug: 'ed9d9d88-0fdf-5166-b068-8d915dcdcebd'

draft: 0
---

Создание и восстановление бинарной резервной копии конфигурации {{< tag "MikroTik" >}}.

<!--more-->

## Создание

- Сделать бинарную резервную копию конфигурации с именем `SERIAL_NUMBER.2026-03-16.backup` на `flash`:

```
:local sn [/system routerboard get serial-number]; :local date [/system clock get date]; /system backup save dont-encrypt=yes name="/flash/$sn.$date"
```

- Сделать бинарную резервную копию конфигурации с именем `SERIAL_NUMBER.2026-03-16.backup` на `sd1`:

```
:local sn [/system routerboard get serial-number]; :local date [/system clock get date]; /system backup save dont-encrypt=yes name="/sd1/$sn.$date"
```

- Сделать бинарную резервную копию конфигурации с именем `SERIAL_NUMBER.2026-03-16.backup` на `sd1-part3` из статьи {{< uuid "4b37dd8e-a96f-5ba0-bb2a-96da70bb3942" >}}:

```
:local sn [/system routerboard get serial-number]; :local date [/system clock get date]; /system backup save dont-encrypt=yes name="/sd1-part3/$sn.$date"
```

- Сделать зашифрованную бинарную резервную копию конфигурации с именем `SERIAL_NUMBER.2026-03-16.backup` на `flash` с паролем `pa$$word`:

```
:local sn [/system routerboard get serial-number]; :local date [/system clock get date]; /system backup save name="/flash/$sn.$date" password="pa$$word"
```

## Восстановление

- Восстановить бинарную резервную копию конфигурации с именем `GW1.2026.03.16.00.backup` с `flash`:

```
/system backup load name="/flash/GW1.2026.03.16.00.backup" password=""
```

- Восстановить бинарную резервную копию конфигурации с именем `GW1.2026.03.16.00.backup` с `sd1`:

```
/system backup load name="/sd1/GW1.2026.03.16.00.backup" password=""
```

- Восстановить бинарную резервную копию конфигурации с именем `GW1.2026.03.16.00.backup` с `sd1-part3` из статьи {{< uuid "4b37dd8e-a96f-5ba0-bb2a-96da70bb3942" >}}:

```
/system backup load name="/sd1-part3/GW1.2026.03.16.00.backup" password=""
```

- Восстановить зашифрованную бинарную резервную копию конфигурации с именем `GW1.2026.03.16.00.backup` с `flash` и паролем `pa$$word`:

```
/system backup load name="GW1.2026.03.16.00.backup" password="pa$$word"
```
