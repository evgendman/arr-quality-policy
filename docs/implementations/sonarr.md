# Реализация универсальной схемы в Sonarr

Каталог Sonarr содержит **55 Custom Formats**:

| Группа | Количество |
|---|---:|
| Voice | 41 |
| Src | 8 |
| Format | 5 |
| Extra | 1 |
| **Всего** | **55** |

Оценки применены к профилю **1080p RU**.

## Почему условия источников Sonarr отличаются

В Sonarr Source BDRip — отдельная категория, а Blu-ray Disk и Remux находятся в объединённой категории. Поэтому для разделения BDRip, Remux и Disk используются дополнительные условия Release Title.

| Логический тип | Реализация Sonarr | Баллы |
|---|---|---:|
| Blu-ray BDRip | Source BDRip + title regex, требующий Blu-ray/BDRip и исключающий Disk/BDMV/Remux | +120 000 |
| Blu-ray Remux | Source Bluray-Disk/Remux + явный Remux marker | +60 000 |
| Blu-ray Disk | Самостоятельный title-only отрицательный формат | -1 000 000 |
| DVD | Source DVD, нейтральный Src-DVD | 0 |
| DVD Disk | Title-only отрицательное правило | -1 000 000 |
| HDTV/SDTV | Source HDTV/SDTV | +80 000 |
| WEB-DL | Source WEB-DL | +140 000 |
| WEBRip | Source WEBRip | +100 000 |

Нейтральный Src-DVD не включает DVD обратно в профиль качества. Допустимость самого качества — отдельная настройка Quality Profile.

## Каталог и YAML

- [JSON catalog Sonarr — 55 отдельных JSON](../../recyclarr/catalogs/sonarr-custom-formats-json.tar.gz)
- [Recyclarr YAML Sonarr](../../recyclarr/config/sonarr.yml)
- [Общий settings.yml с providers](../../recyclarr/config/settings.yml)

Sonarr не получает Extra-Theatrical, поскольку этот признак относится к редакции фильма. Extra-HEVC / H.265 остаётся нейтральным.

## Фактическое применение 2026-11-06

Recyclarr v8.8.1 синхронизировал только экземпляр `mini_sonarr_1080p`:

| Действие | Количество |
|---|---:|
| Создано | 32 |
| Обновлено | 4 |
| Без изменений | 19 |
| Удалено | 0 |
| Обновлён профиль 1080p RU | 1 |

Постпроверка подтвердила:

- 62 Custom Formats в базе Sonarr: 55 управляемых и 7 прежних локальных/служебных форматов.
- Все 55 назначений оценок соответствуют целевому YAML; расхождений нет.
- Структура качества, разрешённые качества и пороги профиля не изменились.
- Старые форматы не удалялись благодаря `delete_old_custom_formats: false`.
- Radarr не синхронизировался.

Прежние записи `Bluray-BDRip`, `Bluray-Disk`, `Bluray-Remux`, `HDTV/SDTV`, `SeasonPack`, `WEB-DL`, `WEBRip` сохранены в базе и не входят в новый управляемый каталог.

[Отчёт о Sonarr Sync](../../reports/sonarr-sync-2026-11-06.md) · [Универсальная модель](../policy-model.md)
