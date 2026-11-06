# Группа Src — источники и типы носителей

Группа Src описывает источник/носитель независимо от разрешения. Баллы задают базовое предпочтение при сравнении допустимых вариантов внутри сопоставимой группы качества.

## Универсальная шкала

| Логический источник | Custom Format | Баллы |
|---|---|---:|
| WEB-DL | Src-WEB-DL | +140 000 |
| Blu-ray BDRip | Src-Bluray-BDRip | +120 000 |
| WEBRip | Src-WEBRip | +100 000 |
| HDTV/SDTV | Src-HDTV/SDTV | +80 000 |
| Blu-ray Remux | Src-Bluray-Remux | +60 000 |
| Blu-ray Disk | Src-Bluray-Disk / Src-Bluray-Disk-Title | 0 / -1 000 000 |
| Явный DVD Disk | Src-DVD-Disk | -1 000 000 |
| DVD source в Sonarr | Src-DVD | 0 |

WEB-DL выше BDRip на 20 000. Преимущество источника может быть перекрыто более важным признаком дорожки, например Russian Dubbing +100 000.

## Radarr: Source + Quality Modifier

| Custom Format | Условие | Баллы |
|---|---|---:|
| Src-Bluray-BDRip | Source Blu-ray + Quality Modifier None | +120 000 |
| Src-Bluray-Remux | Source Blu-ray + Quality Modifier Remux | +60 000 |
| Src-Bluray-Disk | Source Blu-ray + Quality Modifier BR-DISK | 0 |
| Src-Bluray-Disk-Title | Release Title regex ниже | -1 000 000 |
| Src-DVD-Disk | Release Title regex ниже | -1 000 000 |
| Src-HDTV/SDTV | Source TV + Quality Modifier None | +80 000 |
| Src-WEB-DL | Source WEB-DL | +140 000 |
| Src-WEBRip | Source WEBRip | +100 000 |

Radarr нативно различает Blu-ray BDRip, Remux и BR-DISK комбинацией Source + Quality Modifier. Качество BR-DISK отключено в текущем профиле; обычный DVD/DVDRip не блокируется выражением полного DVD Disk.

## Sonarr: Source + Release Title conditions

В Sonarr BDRip имеет отдельный нативный класс Source, но Blu-ray Disk и Remux представлены объединённой категорией. Поэтому BDRip и Remux дополнены title-условиями, а Disk защищён отдельным отрицательным Custom Format.

| Custom Format | Условие | Баллы |
|---|---|---:|
| Src-Bluray-BDRip | Source BDRip + Release Title regex, требующий Blu-ray/BDRip и исключающий Disk/BDMV/Remux | +120 000 |
| Src-Bluray-Remux | Source Bluray-Disk/Remux + явный Remux marker в Release Title | +60 000 |
| Src-Bluray-Disk-Title | Release Title regex ниже | -1 000 000 |
| Src-DVD | Source DVD | 0 |
| Src-DVD-Disk | Release Title regex ниже | -1 000 000 |
| Src-HDTV/SDTV | Source HDTV/SDTV | +80 000 |
| Src-WEB-DL | Source WEB-DL | +140 000 |
| Src-WEBRip | Source WEBRip | +100 000 |

Нейтральный Src-DVD не включает DVD обратно в Quality Profile: допустимость качества задаётся отдельно.

## Точные Release Title expressions

**Blu-ray Disk — Radarr и Sonarr, штраф -1 000 000:**

`(?i)\b(?:BDMV|BD[-_. ]?(?:DISK|DISC)|BLU[-_. ]?RAY[-_. ]?(?:DISK|DISC)|(?:FULL|COMPLETE)[-_. ]?BLU[-_. ]?RAY)\b`

**DVD Disk — Radarr и Sonarr, штраф -1 000 000:**

`(?i)\b(?:VIDEO[ ._-]?TS|AUDIO[ ._-]?TS|FULL[ ._-]?DVD|COMPLETE[ ._-]?DVD|DVD[ ._-]?(?:VIDEO(?:[ ._-]?TS)?|ISO|IMAGE|DISC|DISK|FULL|[59])|DVD[ ._-]?R(?:[ ._-]?[59])?)\b`

**Sonarr Blu-ray Remux condition:**

`(?i)\b(?:BD[-_. ]?REMUX|BLU[-_. ]?RAY[-_. ]?REMUX|REMUX)\b`

**Sonarr Blu-ray BDRip condition:**

`(?i)^(?!.*\b(?:REMUX|BDMV|BD[-_. ]?(?:DISK|DISC)|BLU[-_. ]?RAY[-_. ]?(?:DISK|DISC)|(?:FULL|COMPLETE)[-_. ]?BLU[-_. ]?RAY)\b).*\b(?:BLU[-_. ]?RAY|BDRIP)\b`

## Границы

- В Radarr качество DVD-R отключено; обычный DVD/DVDRip остаётся допустимым.
- В текущем Sonarr 1080p RU качество DVD отключено. Наличие Src-DVD не отменяет это ограничение.
- BR-DISK отключено в текущем профиле Radarr; title-правило добавляет защиту по явным дисковым названиям.
- Штраф -1 000 000 превышает теоретическую сумму положительных весов текущего набора; при минимальном пороге 0 явный Disk marker исключает релиз.
- Выражения анализируют только Release Title. Диск без явных маркеров в названии автоматически не обнаруживается.
